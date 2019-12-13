## Training Model Through CVAT
Once you have annotated enough data, you can train a model to pre-annotate rest of your images. This can save a lot of time in annotation. 

1 - Annotate enough images in your CVAT task.  
2 - Go back to your CVAT dashboard and click on `Create New Annotation Model` in that task. You will see a popup with few options.  
3 - Select approprite model type (TensorFlow OD API recommended) and then select the model (i.e ssd-mobilenet-v2-coco-201).  
4 - Select the machine type. A machine with multiple GPUs will speed up your training process.  
5 - Enter optional arguments. See below for more details.  

![CVAT flowchart](https://github.com/onepanelio/images/blob/master/auto-annotation-v.2.0.png)

## Arguments (optional)

You can optionally specify some arguments in the `Arguments` field seperated by `;`. 

Here is a sample: `epochs=100;batch_size=24`. 

- epochs : number of epochs to train your model for. By default, we will train for appropriate number of epochs depending upon the model.
- batch_size : batch size for the training
- initial_learning_rate : initial learning rate for the model. We recommend you do not change this.
- num_clones (default=1): number of gpus to train model on 

If you select a Machine type with 4 GPUs (Tesla V100), the following command can be used:
`epochs=300000;num_clones=4;batch_24;`

- Note that num_clones is 4 because there are 4 gpus available.

## Adding your own base model to CVAT

You can also add your own base models to CVAT via Onepanel.  Please email us at info@onepanel.io to learn how.
