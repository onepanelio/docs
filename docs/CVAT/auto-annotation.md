
# CVAT Pre-annotation using base models

The Code for the App is Hosted [here](https://github.com/onepanelio/demo-app) .
The whole project can be visualized in the block diagram below :
![App Flow Diagram](https://github.com/onepanelio/demo-app/blob/master/assets/mobile_app_flow.png?raw=true)

## Steps


1. Resume [dataset-upload-api](https://c.onepanel.io/onepanel-demo/projects/mobile-demo/overview/onepanel-demo/projects/mobile-demo/workspaces/dataset-upload-api) and  run  video_upload.py to start the API .

The basic idea of file uploads is actually quite simple. It basically works like this:

A ```<form>``` tag is marked with ```enctype=multipart/form-data``` and an ```<input type=file>``` is placed in that form.

The application accesses the file from the files dictionary on the request object.

use the ```save()``` method of the file to save the file permanently somewhere on the filesystem. 
```python
import os
from flask import Flask, flash, request, redirect, url_for
from werkzeug.utils import secure_filename

UPLOAD_FOLDER = '/path/to/the/uploads'
ALLOWED_EXTENSIONS = {'txt', 'pdf', 'png', 'jpg', 'jpeg', 'gif'}

app = Flask(__name__)
app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER 
```
The ```werkzeug.secure_filename()``` is explained a little bit later. The ```UPLOAD_FOLDER``` is where we will store the uploaded files and the ```ALLOWED_EXTENSIONS``` is the set of allowed file extensions.

Next the functions that check if an extension is valid and that uploads the file and redirects the user to the URL for the uploaded file:
```python
def allowed_file(filename):
    return '.' in filename and \
           filename.rsplit('.', 1)[1].lower() in ALLOWED_EXTENSIONS

@app.route('/', methods=['GET', 'POST'])
def upload_file():
    if request.method == 'POST':
        # check if the post request has the file part
        if 'file' not in request.files:
            flash('No file part')
            return redirect(request.url)
        file = request.files['file']
        # if user does not select file, browser also
        # submit an empty part without filename
        if file.filename == '':
            flash('No selected file')
            return redirect(request.url)
        if file and allowed_file(file.filename):
            filename = secure_filename(file.filename)
            file.save(os.path.join(app.config['UPLOAD_FOLDER'], filename))
            return redirect(url_for('uploaded_file',
                                    filename=filename))
    return '''
    <!doctype html>
    <title>Upload new File</title>
    <h1>Upload new File</h1>
    <form method=post enctype=multipart/form-data>
      <input type=file name=file>
      <input type=submit value=Upload>
    </form>
    '''
    ```
```
### Annotation
Once Data is Upload is in the workspace, create a Datset and Pull it into CVAT Workspace and start Annotating.
Dump the annotations into a CVAT XML . Given a CVAT XML and a directory with the image dataset, this script reads the CVAT
XML and writes the annotations in tfrecords format into a given directory in addition
to the label map required for the tensorflow object detection API. Install necessary packages (including tensorflow).

```bash
sudo apt-get update
sudo apt-get install -y --no-install-recommends python3-pip python3-dev
```

``` bash
pip3 install -r requirements.txt
```

### 2. Install the tensorflow object detection API
 If it's already installed you can check your `$PYTHONPATH`and move on to the usage section. 
 Here's a quick (unofficial) guide on how to do that.
 For more details follow the official guide
 [INSTALL TENSORFLOW OBJECT DETECTION API](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md).
 
```bash
# clone the models repository
git clone https://github.com/tensorflow/models.git
```
```bash
# install some dependencies
pip3 install --user Cython
pip3 install --user contextlib2
pip3 install --user pillow
pip3 install --user lxml
pip3 install --user jupyter
pip3 install --user matplotlib
```
```bash
# clone and compile the cocoapi
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
make
cp -r pycocotools <path_to_models_repo>/models/research/
```
```bash
# Protobuf Compilation
cd <path_to_models_repo>/models/research/
protoc object_detection/protos/*.proto --python_out=.
```
```bash
# setup the PYTHONPATH
export PYTHONPATH=$PYTHONPATH:`pwd`:`pwd`/slim
 ```

## Usage

Run the script.

```bash
$python3 converter.py --cvat-xml </path/to/cvat/xml> --image-dir </path/to/images>\
  --output-dir </path/to/output/directory> --attribute <attribute>
```

Leave `--attribute` argument empty if you want the to consider CVAT labels as tfrecords labels,
otherwise you can specify a used attribute name like `--attribute <attribute>`.

Please run `python converter.py --help` for more details.

Once Data is Annotated and Converted to tfrecords, use the Following to train a model using it 
```bash
$python /onepanel/code/models/research/object_detection/legacy/train.py \
--train_dir=/onepanel/code/Custom-Mask-RCNN-using-Tensorfow-Object-detection-API/CP \
--pipeline_config_path=/onepanel/code/Custom-Mask-RCNN-using-Tensorfow-Object-detection-API/mask_rcnn_inception_v2_coco.config

```

### Start the Inference API
Once we’ve retrained our model and exported it to disk, we can host the model as a service. We’ll load the model from disk with a simple function that takes the graph definition directly from the file and uses that to generate a graph. TensorFlow does most of this for us, Resume [dataset-upload-api](https://c.onepanel.io/onepanel-demo/projects/mobile-demo/overview/onepanel-demo/projects/mobile-demo/workspaces/dataset-upload-api) and  run  video_upload.py to start the API .
```python
detection_graph = tf.Graph()
with detection_graph.as_default():
  od_graph_def = tf.GraphDef()
  with tf.gfile.GFile(PATH_TO_CKPT, 'rb') as fid:
    serialized_graph = fid.read()
    od_graph_def.ParseFromString(serialized_graph)
    tf.import_graph_def(od_graph_def, name='')
label_map = label_map_util.load_labelmap(PATH_TO_LABELS)
categories = label_map_util.convert_label_map_to_categories(label_map, max_num_classes=NUM_CLASSES, use_display_name=True)
category_index = label_map_util.create_category_index(categories)


def load_image_into_numpy_array(image):
  (im_width, im_height) = image.size
  return np.array(image.getdata()).reshape(
      (im_height, im_width, 3)).astype(np.uint8)


```
Using Flask, much of the heavy-lifting around configuring a server and handling requests is done for us. After we’ve created a Flask app object:
```python
app = Flask(__name__)
```
Then, we can easily create routes for where our classification service will live. Let’s create a default route to our classify() function that will allow us to pass an image to the endpoint for identification.
```python
@app.route('/')
def uploaded_file(filename):
    PATH_TO_TEST_IMAGES_DIR = app.config['UPLOAD_FOLDER']
    TEST_IMAGE_PATHS = [ os.path.join(PATH_TO_TEST_IMAGES_DIR,filename.format(i)) for i in range(1, 2) ]
    IMAGE_SIZE = (12, 8)

    with detection_graph.as_default():
        with tf.Session(graph=detection_graph) as sess:
            for image_path in TEST_IMAGE_PATHS:
                image = Image.open(image_path)
                image_np = load_image_into_numpy_array(image)
                image_np_expanded = np.expand_dims(image_np, axis=0)
                image_tensor = detection_graph.get_tensor_by_name('image_tensor:0')
                boxes = detection_graph.get_tensor_by_name('detection_boxes:0')
                scores = detection_graph.get_tensor_by_name('detection_scores:0')
                classes = detection_graph.get_tensor_by_name('detection_classes:0')
                num_detections = detection_graph.get_tensor_by_name('num_detections:0')
                (boxes, scores, classes, num_detections) = sess.run(
                    [boxes, scores, classes, num_detections],
                    feed_dict={image_tensor: image_np_expanded})
                vis_util.visualize_boxes_and_labels_on_image_array(
                    image_np,
                    np.squeeze(boxes),
                    np.squeeze(classes).astype(np.int32),
                    np.squeeze(scores),
                    category_index,
                    use_normalized_coordinates=True,
                    line_thickness=8)
                im = Image.fromarray(image_np)
                im.save('uploads/'+filename)

    return send_from_directory(app.config['UPLOAD_FOLDER'],
                               filename)
```
Using the decorator syntax to define the route, it will configure the service so that our uploaded_file() function will be called every time someone hits the root of our service address. We said we wanted users to be able to specify a file to be identified so we’ll store that as a parameter from the request:
```python
file_name = request.args['file']
``
In an actual app, we’d probably populate this from a form attachment or URL. For our example, we’ll simply let users specify a path to the file that they want to be identified.

We can then read the image file and turn it into a tensor to be used as input to the graph we loaded previously. The base script included a number of useful functions including read_tensor_from_image_file() which will take the image file and turn it into a tensor to use as input by using a small custom TensorFlow graph.

Running the inference on our graph with this image is again quite straightforward:
```python
       (boxes, scores, classes, num_detections) = sess.run(
                    [boxes, scores, classes, num_detections],
                    feed_dict={image_tensor: image_np_expanded})
    ```
In this line, the variable t represents the image tensor that was created by read_tensor_from_image_file() function. TensorFlow will then take that image and run the new retrained model to generate predictions.

Those predictions come as a series of probabilities that indicate which of the classes (poodle, pug, or wiener dog) is the most likely. Since this is just a prediction service, it will simply return a JSON representation of the arrays.

Inside our script we can start our service with:
```python
app.run(debug=True, port=5000)
```
Then, if we want to launch the script from the command line, all we have to do is run python app.py and it will initialize and start running on port 5000.
### Using the Service

We can now use this service either by visiting it in a web browser or generally making any REST call on that port. For an easy test we can access it using following code snippet:
```python
import os
import requests
url = 'http://0.0.0.0:5000/onepanel-demo/projects/mobile-demo/workspaces/classification/api/upload'
path_img='/onepanel/code/FlaskObjectDetection/centaur_2.mpg'
with open(path_img, 'rb') as img:
  name_img= os.path.basename(path_img)
  files= {'file': (name_img,img,'multipart/form-data',{'Expires': '0'}) }
  with requests.Session() as s:
    r = s.post(url,files=files)
    print(r.status_code)
```

### Download APP 
Download the Android app by scanning the QR ![Android App](https://github.com/onepanelio/demo-app/raw/master/assets/androidapp.png)
 or click on this [Link](http://bit.ly/onepanel_v_0_0_4_5)
