To create a dataset from AWS S3 buckets, you will need to first launch a Workspace.  Make sure to select a storage size that is at least as big as your dataset.

Once the Workspace is launched, set your AWS credentials:  
```bash
export AWS_ACCESS_KEY_ID=<key-id>  
export AWS_SECRET_ACCESS_KEY=<secret>
```
Then, download the bucket into a local folder:  
```bash
aws s3 sync s3://<s3-bucket-name>/ /onepanel/input/datasets/<your-dataset-name>
```
Then, cd  into that folder and create the Onepanel dataset:
```bash
cd /onepanel/input/datasets/<your-dataset-name>
onepanel datasets init
onepanel datasets push -b
```

**Note:**  
Setting the -b option on `onepanel push`, will run upload in the background. You will receive an email when upload is complete.