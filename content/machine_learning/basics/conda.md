---
title: "Conda cheat sheet"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Resources
* https://docs.conda.io/projects/conda/en/4.6.0/_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf
* https://docs.conda.io/projects/conda/en/latest/commands.html#conda-vs-pip-vs-virtualenv-commands
* https://anaconda.org/


### Managing environment

* Use **base** environment: `conda activate`
* Deactivate enviornment: `conda deactivate`
* List all conda environments: `conda info --envs`
* Create a new environment: `conda create --name pytorch`
* Active the new environment: `conda activate pytorch`
* Install a package in the newly created environment: 
```bash 
conda install pytorch torchvision torchaudio -c pytorch
conda install jupyterlab -c conda-forge
```
* List all packages in an environment: `conda list`
* List all packages installed into the environment 'myenv': `conda list -n myenv`
* Save packages for future use: `conda list --export > package-list.txt`
* Reinstall packages from an export file: `conda create -n myenv --file package-list.txt`
* Create a new environment with Python 3.10: `conda create --name py310 python=3.10`
* Make exact copy of an environment: `conda create --clone py310 --name py310-2`

Note:    
* `-c` stands for channel: Location of where the packages are stored, i.e.: http://conda.anaconda.org/. For example: pytorch -> https://anaconda.org/pytorch, conda-forge -> https://anaconda.org/conda-forge.



### Conda installation

* Download and run installers based on OS from https://docs.conda.io/en/latest/miniconda.html
* Verify it is running `conda --version`
* Update conda `conda update conda`


### Conda vs pip

**Pip** is the Python Packaging Authority’s recommended tool for installing packages from the Python Package Index. Only works with Python. Relies on `pipenv` or `virtualenv` or `venv` to isolate environment. Contains over 150,000 packages.

**Conda** is a cross platform package and environment manager that installs packages in any language (python, C, C++, etc.). Contains 15,000 packages. Can install pip for PyPi packages.

Resources:   
* https://docs.conda.io/projects/conda/en/latest/commands.html#conda-vs-pip-vs-virtualenv-commands
* https://www.anaconda.com/blog/understanding-conda-and-pip

