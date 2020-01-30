## Semi-automatic Annotation on CVAT

You can use your TensorFlow or OpenVINO model to pre-annotate your data. This can save you a lot of time since you don't have to annotate images from scratch. On Onepanel, you can leverage these features to pre-annotate your bounding boxes or polygon masks. You can also use Object Tracking to track objects in a sequence of frames.

## Semiautomatic Annotation of Polygon Masks (Segmentation)

On your CVAT dashboard, go to a task where you would like to run this pre-annotation model on, find `Run Auto Segmentation` button and click on it. This will use provided Mask RCNN model to pre-annotate masks on your images.
Please note that the Mask RCNN model is a compute intensive model. It woudl require more than 8GB of ram. So, if you want to use this feature on Onepanel, make sure you use CPU with 32 GB ram or any GPU instance.
