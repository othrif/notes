---
title: "Creating a python package"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
Documentation: https://packaging.python.org/tutorials/packaging-projects/

### Creating a package

Important packages to create python libraries: `pip, setuptools, wheel`

The following are the contents of the two files needed to create a package:
#### File 1: pyproject.toml

``` xml
[build-system]
requires = [
    "setuptools>=42",
    "wheel"
]
build-backend = "setuptools.build_meta"

```

#### File 2: setup.py

``` python
import setuptools

# If you have a README.md:
# with open("README.md", "r", encoding="utf-8") as fh:
#    long_description = fh.read()

setuptools.setup(
    name="example-pkg-YOUR-USERNAME-HERE",
    version="0.0.1",
    author="Example Author",
    author_email="author@example.com",
    description="A small example package",
    long_description="long_description",
    long_description_content_type="text/markdown",
    url="https://github.com/pypa/sampleproject",
    project_urls={
        "Bug Tracker": "https://github.com/pypa/sampleproject/issues",
    },
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
    install_requires=[
        'click',
        'grpcio',
        'path',
        'requests',
        'tensorflow',
        'keras',
        'matplotlib',
        'tqdm',
        'click-config-file',
        'black',
        'typing_extensions',
        'grpcio-tools'
    ],
    package_dir={"": "src"},
    packages=setuptools.find_packages(where="src"),
    python_requires=">=3.8",
)

```

### Building the package

``` bash
python -m pip install --upgrade build
python -m build
```

You get a `whl` wheel distribution file that you can upload to your favorite package host (Cloudsmith, Pypi, etc.)

### Test within the package locally using `pipenv`

In a pipenv environment using the option:
`-e, --editable <path/url>   Install a project in editable mode (i.e. setuptools "develop mode") from a local project path or a VCS url.`

``` bash 
pipenv install -e .
pipenv shell
python 
```

then in python
``` python
from package_inside_src import file_inside_package
my_instance = file_inside_package.class_inside_file("arg1", "arg2")
my_instance.analyze()
```

### Test within the package locally using `pip`

If you just need to test whether pip install works from the built package, you can create it and then use pip to install it from local filesystem.
``` bash
python setup.py sdist
pip install dist/mypackage-1.0.tar.gz
```
If you have been running `python setup.py install` already, ensure you run:
``` bash 
pip uninstall mypackage
```

### Test outside the package from remote distribution repo

Create a new repo and pip install your package:
``` bash 
mkdir test_example-pkg-YOUR-USERNAME-HERE
```

Create a Pipfile with the contents
``` python
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]
example-pkg-YOUR-USERNAME-HERE = "==0.0.6"

[dev-packages]
black = "==20.8b1"

[requires]
python_version = "3.9"

[scripts]
fmt = "black --config Pipfile ."
lint = "black --check --config Pipfile ."

[tool.black]
max-line-length = 120
exclude = '''
(
/(
\.eggs         # exclude a few common directories in the
| \.git        # root of the project
| deactivate
| \.venv
)/
# the root of the project
)
'''
```

Then test it in pipenv:
``` bash 
pipenv install
pipenv shell
python
```

In python:
``` python
from package_inside_src import file_inside_package
my_instance = file_inside_package.class_inside_file("arg1", "arg2")
my_instance.analyze()
```
