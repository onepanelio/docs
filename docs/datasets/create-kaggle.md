*"How do I create a Onepanel dataset from Kaggle using their API all in the cloud?"*

Creating a Onepanel dataset from a Kaggle dataset using the Kaggle API is easy and can be accomplished in a few steps

First, create a Onepanel workspace with storage that is bigger than the Kaggle dataset you're downloading.

Next, open JupyterLab or Onepanel terminals and create the Onepanel dataset, ideally in the `/onepanel/input` folder:
```bash
cd /onepanel/input
onepanel datasets create <dataset-name>
cd <dataset-name>
```
Then, set Kaggle credentials:
```bash
export KAGGLE_USERNAME=datadinosaur
export KAGGLE_KEY=xxxxxxxxxxxxxx
```
Now you can download Kaggle competition files or datasets as follows:
```bash
kaggle datasets download zillow/zecon
```
Refer to the [official Kaggle API documentation](https://github.com/Kaggle/kaggle-api#commands) for additional commands and information.

Finally, push your files to the Onepanel code repo:
```bash
onepanel datasets push
```