---
title: "Using pyenv and upgrading python"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Update pyenv

To pick up the latest python versions for example to get `3.9.2`

``` bash
cd /home/`whoami`/.pyenv/plugins/python-build/../.. && git pull && cd -
pyenv install 3.9.2
```


### Update python from 3.8.5 to 3.9.6

``` bash 
pip list | awk '{print $1}' > /tmp/requirements.txt # list of all your packages in the current python version
brew upgrade
pyenv install 3.9.6
eval "$(pyenv init --path)" # add in .zshrc or .bashrc
pyenv global 3.9.6
pip install -r /tmp/requirements.txt
```

### Working with pyenv
* Note all my old packages worked in 3.8.5
* good review article: https://mungingdata.com/python/how-pyenv-works-shims/
* https://realpython.com/intro-to-pyenv/

``` bash
brew upgrade
pyenv install --list | grep " 3\.9"
pyenv versions
eval "$(pyenv init --path)" # add in .zshrc or .bashrc
pyenv global 3.9.6  # set the global python
cat ~/.pyenv/version # Global python version
python -m test # test your python 
pyenv local 3.6.11 # set a python version for a specific directory
cat /tmp/pyenv_test/.python-version # local python version
ls ~/.pyenv/versions/3.6.11/lib/python3.6/site-packages # all packages code location and what is installed
pyenv uninstall 3.6.11 # uninstall python versions you do not want
pyenv shell 3.8.5 # Change python version
echo $PYENV_VERSION # gives you the python version
```

###  Install all packages from old version to new
``` bash
pyenv shell 3.8.5
pip list | awk '{print $1}' > /tmp/requirements.txt
pyenv shell 3.9.6
pip install -r /tmp/requirements.txt
```

### pyenv and virtual environment

``` bash 
brew install pyenv-virtualenv
eval "$(pyenv virtualenv-init -)" # add in .zshrc or .bashrc
# pyenv virtualenv <python_version> <environment_name>
pyenv virtualenv 3.9.6 myproject # create virtual environment
pyenv local myproject # activate env
pyenv which python # check that you are in the env
```

### Working with multiple environments

``` bash 
# Project 1
$ cd ~/project1/
$ pyenv which python
/usr/bin/python
$ pyenv virtualenv 3.6.8 project1
# ...
$ pyenv local project1
$ python -V
/home/realpython/.pyenv/versions/project1/bin/python
# Outside of folder is normal python
$ cd $HOME
$ pyenv which python
/usr/bin/python

# Project 2
cd ~/project2/
pyenv virtualenv 3.8-dev project2
pyenv local project2

# Result
$ cd project2/
$ python -V
Python 3.8.0a0
$ cd ../project1
$ python -V
Python 3.6.8
```
