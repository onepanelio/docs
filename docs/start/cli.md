## Installation
Onepanel CLI is available on <a href="https://pypi.org/project/onepanel" target="_blank">pypi</a> and works on Windows, MacOS and Linux.

To install Onepanel's CLI via pip :

```bash
pip install -U onepanel
```

We recommend installing onepanel into a python virtual environment, or a conda environment if you'd prefer.

Example installation for python virtual environment
```bash
pip[pip3] install virtualenv
mkdir folder_to_hold_virtual_python
cd folder_to_hold_virtual_python
virtualenv venv_2_7_16[<folder_that_tells_you_what_venv>]
cd venv_2_7_16
source bin/activate
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

Alternatively, you can create an [access token](/integrations/access-tokens/#create-access-token) and then login as follows:

```bash
onepanel login -t <access-token>
```

## Check version

```bash
onepanel --version
```

## Help and documentation

!!! info "Info"
    See [CLI documentation](/cli/) for additional commands

You can add `--help`  to any command to view information about its syntax and options, some examples:

```bash
onepanel jobs --help
onepanel jobs create --help
```