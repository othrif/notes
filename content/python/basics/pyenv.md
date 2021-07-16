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
* Note all my old packages worked in 3.8.5
* good review article: https://mungingdata.com/python/how-pyenv-works-shims/

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
