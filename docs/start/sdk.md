## Installation
Onepanel SDK is available as soon as you install [Onepanel CLI](/start/cli)

!!! note "Note" 
    SDK is pre-installed if you are using Onepanel Workspaces or Jobs.

## Authentication

The recommended way to authenticate in Onepanel's SDK is to use an access token, you can create an access token as shown below:

![Screenshot](/assets/img/access-token.gif)

Then you can authenticate in the SDK as follows:

```python
from onepanel.sdk import Client

# with username/access_token
client = Client(username='<username>', access_token='<access token>')

# or with email/access_token
client = Client(email='<email>', access_token='<access token>')

```

## Examples
