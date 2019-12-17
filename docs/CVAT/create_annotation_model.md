## Why Pre-Annotate?
Pre-annotation will cut the time to annotate large amounts of data by orders of magnitude.  The idea is simple, annotate once then QC each successive dataset after.
Once you have annotated enough data, you can train a model to pre-annotate the rest of your images with a few button clicks.

## Training Model Through CVAT

1 - Annotate enough images in your CVAT task.  
2 - Go back to your CVAT dashboard and click on `Create New Annotation Model` in that task. You will see a popup with a few options.  
3 - Select the appropriate model type (TensorFlow OD API recommended) and then select the model (i.e ssd-mobilenet-v2-coco-201).  
4 - Select the machine type. A machine with multiple GPUs will speed up your training process.  
5 - Enter optional arguments. See below for more details.  

![CVAT flowchart](../assets/img/auto-annotation-v.2.0.png?raw=true)

## Arguments (optional)

You can optionally specify some arguments in the `Arguments` field seperated by `,`. 

Here is a sample: `epochs=100,batch_size=24`. 

- epochs : number of epochs to train your model for. By default, we will train for an appropriate number of epochs depending upon the model.
- batch_size : batch size for the training
- initial_learning_rate : initial learning rate for the model. We recommend you do not change this.
- num_clones (default=1): number of GPUs to train the model 

If you select a Machine type with 4 GPUs (Tesla V100), the following command can be used:
`epochs=300000,num_clones=4`

- Note that num_clones is 4 because there are 4 GPUs available.

## Choose a Model to Train

You can train any of the models that we support. Here, we provide a brief explanation on how to choose one model over another based on your needs. Some models are faster than other, whereas some are more accurate than others. We hope this information will help you choose the right model for your task.

* SSD-based networks such as `ssd-mobilenet-v2` are faster than faster-rcnn based models. However, they are not as accurate as faster-rcnn based models. This model is generally recommended since its accurate and fast enough. If you don't know much about your data or the complexity of your data, then we recommend you go with this model.

* Apart from this, we also support few faster-rcnn models. All of these models are almost similar except the backbone they use for the feature extraction. These backbones are, in increasing order of complexity (i.e more layers), ResNet50, ResNet101, InceptionResNetV2. As the model complexity increases the computation requirement also increases. If you have very complicated data (i.e hundreds of annotations in one image), then it is recommended that you choose complex model (i.e InceptionResNetV2).

* Faster-rcnn models are generally expected to be more accurate than ssd ones. However, sometimes you are better off with ssd models if your data is easy to learn (i.e 1 or 2 bounding box per image).

* If you are using `frcnn-nas-coco`, then please choose a machine with at least 2 GPUs as this model requires more memory. A machine with 1 GPU will throw an error.

* Note that we don't support Yolo and MaskRCNN models yet.

## Adding your own base model to CVAT

You can also add your own base models to CVAT via Onepanel.  Please email us at info@onepanel.io to learn how.

## Open source code

You can find the code that triggers dataset creation, base model pulling, model training, and model conversion here:

https://github.com/onepanelio/cvat-training
