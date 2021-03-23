---
title: "Using pipenv and saving python environment"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Pipenv workflow
If the `Pipfile` exists, run 
``` bash  
pipenv install
```
To run, 
``` bash 
pipenv run <command>
```
To enter a shell within the environment
``` bash 
pipenv shell
```

To add a package to your new project
``` bash 
pipenv install <package>
```

or edit the `Pipfile` directly, here added package `requests`
``` python
[[source]]
url = "https://pypi.python.org/simple"
verify_ssl = true
name = "pypi"

[packages]
requests = "*"

[dev-packages]
```

### Save python environment
``` bash 
pipenv install <all packages i need>
pipenv lock --requirements > requirements.txt
```

### Install a specific version of python
``` bash 
pipenv --python X.Y
```

### Specify verion of a pckage
``` bash 
pipenv install requests~=1.2
```

### Install from a website
``` bash 
# Need to keep the correct python 3.9 version -> 39
pipenv install https://download.pytorch.org/whl/cu111/torch-1.8.0%2Bcu111-cp39-cp39-linux_x86_64.whl

# below runs but does not save it to Pipfile
pipenv run pip install torch==1.8.0+cu111 -f https://download.pytorch.org/whl/torch_stable.html
```

### Install from git
``` bash 
pipenv install -e git+https://github.com/requests/requests.git@v2.20.1#egg=requests
```
