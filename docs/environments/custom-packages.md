Onepanel comes pre-installed with many libraries for machine learning and deep learning. But in case you need additional packages, you can also install custom packages using `pip`, `conda` or `apt-get`.

## Installing PyPI packages
You can install PyPi packages in two ways:

- Install using:
```
pip install <package-name>
```
- Install persistent packages using a `requirements.txt` file that you commit into your repository.

Refer to <a href="https://pip.pypa.io/en/stable/user_guide/#installing-packages" target="_blank">pip documention</a> or <a href="https://pip.pypa.io/en/stable/user_guide/#requirements-files" target="_blank">requirements.txt documentation</a> for more information.

## Installing Conda packages
You can install Conda packages as follows:

```
conda install <package_name>
```

!!! note "Note" 
    Your PyPi packages are installed in the same Conda environment.

Refer to <a href="https://conda.io/docs/user-guide/tasks/manage-pkgs.html" target="_blank">conda install documentation</a> for more information and additional commands.

## Installing APT Packages
You can also install app packages using apt-get  as follows:

```
sudo apt-get install <package-name>
```

Refer to <a href="http://manpages.ubuntu.com/manpages/xenial/en/man8/apt-get.8.html" target="_blank">apt-get documentation</a> for more information and additional commands.