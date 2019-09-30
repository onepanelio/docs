## Installation
Onepanel SDK is available as soon as you install [Onepanel CLI](/start/cli)

!!! note "Note" 
    SDK is pre-installed if you are using Onepanel Workspaces or Jobs.

## Authentication

The recommended way to authenticate in Onepanel's SDK is to use an access token, you can create an [access token](/integrations/access-tokens/#create-access-token) and authenticate in the SDK as follows:

```python
from onepanel.sdk import Client

# with username/access_token
client = Client(username='<username>', access_token='<access token>')

# or with email/access_token
client = Client(email='<email>', access_token='<access token>')

```

## Example: create a job

!!! example "Example"
    See the <a href="https://github.com/onepanelio/sdk/blob/master/example.ipynb" target="_blank">SDK notebook</a> for a complete example
    

```python
from onepanel.models import Job

from onepanel.sdk import Client

# login with email/access_token
client = Client(email='<email>', access_token='<access token>')

# create a job
job = Job()

job.name = '<job-name>'
job.project.uid = '<your-project-uid>'
job.command = '<command>'
job.machine_type.uid = '<machine-type-uid>'
job.environment.uid = '<environment-uid>'
job.volume_type.uid = '<volume-type-uid>'

# create a job by uploading code from current directory
job_uid = client.jobs.create(job)
```
