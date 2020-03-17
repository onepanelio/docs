## Creating New Tasks
Once you're inside CVAT dashboard, you can create new tasks to start annotating. You will find a Create New Task button on top, clicking on it will open up a new pop up window as follows:
![Create New Task](../assets/img/1.PNG?raw=true)

Now, you give this task a name you like. Then, labels that you are interested in annotating (i.e car, bicycle). You also need to select the source of your data (images). You can upload from your local machine or use data uploaded to Onepanel dataset. In the later case, you need to select the Share option. Now, go ahead and click on Select files. If you selected Share, then your dataset will be inside /input/datasets/<username>. After you select the images, hit submit to create a new task.

## Manual Annotation
Once you have created a new task, you can start annotating your data. CVAT supports points, box, polylines, polygons for annotation. So, the first thing you should do is go to bottom-left of the window and select the type of annotation you want as shown below. 
![Select Annotation](../assets/img/2.PNG?raw=true)

### Points
If you want to annotate points, then select Points instead of Box which is a default choice. Once you select points, you can start annotating by clicking on Create Shape, clicking on image where you want to put the point and then click on stop shape. Or alternatively you can use keyboard shortcut N instead of Create Shape/Stop Shape. Make sure you periodically save your annotation by pressing ctrl + s.

### Bounding Box
The same process follows for bounding boxes. Select Box and press N to start annotating once done, press N to finish annotation.
![Annotation](../assets/img/3.PNG?raw=true)

If you want to change the class of an object. Finish drawing bounding box around an object, then go to right sidebar and change the class from a dropdown menu. The same has been heighted in blue color in above picture.

### Polygons
Similarly, select polygons or polylines and follow same procedure for annotation.

### Semi-automatic Annotation of Polygon
We also support a specific type of pre-annotation called Extreme Points to Segmentation. In this case, you don’t need to select complete boundary of an object. Instead, you just put some points (i.e 4) around an object then hit N. It will find perfect boundary automatically. For this to work, you need to select Auto Segmentation from the bottom left option.

## Using Pre-Annotation Model
Onepanel’s CVAT supports a feature to pre-annotate images for common objects. In order to use any pre-annotation feature, you first need to upload the model. By default, we provide a default model for bounding box annotation. Click on Model Manager, and give a name to it. Click on select files -> input -> models -> cvat-default and select both files. Hit submit to upload the model. For segmentation model, you first need to attach the default to your workspace. For this, click on your workspace name on top, you will find an option to Add Dataset. Then, search for maskrcnn-default, click on Add. Now, go to Model Manager and upload this model, but make sure you select Segmentation instead of TF Annotation in radio button. Also, you can found model in input - > dataset -> onepanel-demo -> maskrcnn-default. Select both files.
![Model Manager](../assets/img/6.PNG?raw=true)

Above image shows how you can attach dataset to the workspace. Below image shows how you can upload your models to model manager.

![Uploaded Models](../assets/img/7.PNG?raw=true)

Once you have the models in Model manager. Click on Run TF Annotation or Run Auto Segmentation depending upon your need. Then, you will be asked to select the model you want to use for pre-annotation. You can also control the class mapping from your task’s classes to model’s classes. Once done, click on start to start pre-annotation. Once it's done, you can click on the task link to access the annotation.

## Training New Annotation Model
Onepanel also allows you to further finetune your model for annotation. Once you are done with your annotation or adjustment to pre-annotation, you can train a new model on it. To do so, go to dashboard -> Create Annotation Model.

There, you can select the Tensorflow OD API for bounding boxes or Mask RCNN for segmentation.

For TensorFlow OD API, we support multiple models. In fact, its dynamic. You can also train the model you like as long as it is supported by Tensorflow Object Detection API. 

![Create Annotation Model](../assets/img/4.PNG?raw=true)

### How to choose the model:
If you are unsure about which model to use, we usually suggest ssd-mobilenet-v2 since ssd-based models are faster and accurate enough for most of the work. Faster-rcnn (frcnn) models are more accurate in general but they will be relatively slow during training as well inference. If accuracy is more important to you, we suggest you go with frcnn-res101-coco model.






