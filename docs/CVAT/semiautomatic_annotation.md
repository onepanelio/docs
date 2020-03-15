## Semi-automatic Annotation on CVAT

You can use your TensorFlow or OpenVINO model to pre-annotate your data. This can save you a lot of time since you don't have to annotate images from scratch. On Onepanel, you can leverage these features to pre-annotate your bounding boxes or polygon masks. You can also use Object Tracking to track objects in a sequence of frames.

## Uploading Your Model on CVAT
Before using any type of semi-automatic annotation, you will need to upload your model on CVAT Model Manager. To upload your model, go to your CVAT dashboard and click on Model Manager. A pop window will appear where you can give a name to your model, select the source of your files (local or onepanel datasets), and select files. For TF Annotation and Segmentation, you will need two files- model and classes.csv. For TF Annotation, the model should be Tensorflow Frozen Graph (.pb). For Segmentation, it should be keras model (.h5).

## Semi-automatic Annotation of Bounding Boxes
The first step is to upload your model on CVAT or use our default model which is inside input/models/cvat-default. Now, click on Run TF Annotation. A pop up will appear where you can select the model you want to use for pre-annotation. Once you select the model, an automatic class mapping will appear, you can modify it if you want. Once done, click on Start. Once it is done, you can go into your task and check out the pre-annotation.

## Semi-automatic Annotation of Polygon Masks (Segmentation)
On your CVAT dashboard, go to a task where you would like to run this pre-annotation model on, find `Run Auto Segmentation` button and click on it. Similar to above, a list of models will appear. Select the model and hit Start. Your pre-annotation will be started.
Please note that the Mask RCNN model is a compute intensive model. It would require at least a single GPU machine.
