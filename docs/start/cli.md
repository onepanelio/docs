## Installation
Onepanel CLI is available on <a href="https://pypi.org/project/onepanel" target="_blank">pypi</a> and works on Windows, MacOS and Linux.

To install Onepanel's CLI via pip :

```bash
pip install -U onepanel
```

!!! note "Note" 
    CLI is pre-installed if you are using Onepanel Workspaces or Jobs.

!!! tip "Tip" 
    The CLI is compatible with Python 2.7.x and Python >= 3.6.x, if you have both versions installed, you will need to use pip3 for Python >= 3.6.x.

## Authentication

You can connect your Onepanel account to CLI by using the `login` command where you'll be prompted for your email and password:

```
onepanel login
```

Alternatively, you can create an access token as shown below:

![Screenshot](/assets/img/access-token.gif)

And then login as follows:

```bash
onepanel login -t <access-token>
```

## Check version

```bash
onepanel --version
```

## Help and documentation

You can add `--help`  to any command to view information about its syntax and options, some examples:

```bash
onepanel jobs --help
onepanel jobs create --help
```