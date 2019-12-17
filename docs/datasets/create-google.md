To create a dataset from Google Cloud Storage (GCS) buckets, you will need to first launch a Workspace.  Make sure to select a storage size that is at least as big as your dataset.

Once the Workspace is launched, install `gsutil`:
```bash
curl https://sdk.cloud.google.com | bash
```
Once installation is complete, restart shell:
```bash
exec -l $SHELL
```
Then, you need to either login with your personal account:
```bash
gcloud auth login
```
or you can alternatively login using a [service account](https://cloud.google.com/sdk/gcloud/reference/auth/activate-service-account).  
Once logged in, you can download the bucket into a local folder:
```bash
gsutil cp gs://<gs-bucket-name>/ /onepanel/input/datasets/<your-dataset-name>
```
Then, cd  into that folder and create the Onepanel dataset as follows:
```bash
cd /onepanel/input/datasets/<your-dataset-name>
onepanel datasets init
onepanel datasets push -b
```
**Note:**  
Setting the -b option on `onepanel datasets push` , will run your upload in the background. You will receive an email when the upload is complete.