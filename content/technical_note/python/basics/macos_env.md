---
title: "Python 3 in MacOS"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Change python to point to python3 by default

``` bash 
ls -l /usr/local/bin/python*
ln -s -f /usr/local/bin/python3.7 /usr/local/bin/python
```

### Which Python version

``` bash 
python -V
```

### Install package
``` bash 
pip install SomePackage            # latest version
pip install SomePackage==1.0.4     # specific version
pip install 'SomePackage>=1.0.4'     # minimum version
pip install SomePackage>=2.0.0,<3.0.0 # Install the latest 2.x release 
pip install SomePackage[extras] # Install package and extras
pip install SomeProject@git+https://git.repo/some_pkg.git@1.3.1 # from version control system
```

### Upgrade package
``` bash 
pip install SomePackage --upgrade
```

### Main packages used

``` bash 
pip install numpy
pip install scipy
pip install scikit-learn
pip install matplotlib
pip install pandas
pip install jupyter notebook
```

### Upgrade pip
``` bash 
python -m pip --version # check version
python -m pip install --user --upgrade pip
```

### Working with virtual environment with `venv`
It is recommended to work in virtual environment to not have comflicts between different packages. This can be done using `venv`. The second argument `env` is the location to create the virtual environment in that folder. Generally, you can just create this in your project and call it env. Make sure to add it to `.gitignore`.
``` bash 
python3 -m venv env
source env/bin/activate
which python # should point to the virtual environment env/bin/python
deactivate # leave virtual environment
```

Installing packages in `venv` is similar to the above:
``` bash 
pip install SomePackage 
```

More importantly it allows you to specify which version to install:
``` bash 
pip install SomePackage

```

Using requirements file `requirements.txt`:
``` python
requests==2.18.4
google-auth==1.1.0
```
Install with: 
``` bash 
pip install -r requirements.txt
```
Freeze dependencies after completing all installation of packages (a way to get the requirement file):
``` bash 
pip freeze
```

### Installing kite for auto-completion in Jupyter
``` bash 
pip install jupyter-kite
jupyter labextension install "@kiteco/jupyterlab-kite"
```

If you get the error 
> Exception: Jupyter command `jupyter-lab` not found.

then: 
``` bash 
pip uninstall -y jupyterlab
pip install jupyterlab
export PATH=$PATH:/usr/local/Cellar/python/3.7.6_1/Frameworks/Python.framework/Versions/3.7/bin
pip install jupyter-kite
jupyter labextension install "@kiteco/jupyterlab-kite"
```
