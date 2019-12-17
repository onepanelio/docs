You can download files from Google Drive as follows.  We recommend you only use this process for non-sensitive data.

Download the Google Drive CLI Client:
```bash
go get github.com/prasmussen/gdrive
```
Then run the following command:
```bash
gdrive list
```
Follow the instructions on the screen.
You can then download any folder as follows:
```bash
gdrive download <folder-id> --recursive
```
To see a list of available gdrive :
```bash
gdrive help
```
See [Creating Datasets](/datasets/create) for instructions on creating a Onepanel Dataset from this data.

##Alternative option  
```bash
pip install gdown
gdown --id <google file id here>
```