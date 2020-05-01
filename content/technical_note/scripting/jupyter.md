---
title: "Jupyter shortcuts and installation"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---

# Jupyter shortcuts

Symbol         | Action
-------------- | -------------
y              | cell format -> code  
m              | cell format -> Markdown  
a              | Add cell above  
b              | Add cell below  
c              | copy cell  
v              | paste cell  
x              | cut cell  
d d            | delete cell  
z              | undo  
shift+z        | redo  
`<space><space>` | new line
`---`            | horizontal line


---
# Jupyter kernels in MacOS

Jupyter kernels are located in: `~/Library/Jupyter/kernels`

List all kernels with: `jupyter kernelspec list`


---

# Jupyter installation with C++ 

C++ kernel for Jupyter is available via `xeus-cling`. Here is the documentaiton: [xeus.readthedocs.io](https://xeus.readthedocs.io/en/latest/installation.html)

- Download a `miniconda` from here: https://docs.conda.io/en/latest/miniconda.html and installed it.
- Install `xeus-cling` with `conda`: `conda install -c conda-forge xeus-cling`
- Installation of `miniconda` will alter your `python` environment to `conda`. I removed it from the path by only keeping `source ~/.bashrc` in `~/.bash_profile` and removing all other lines changing the `PATH` to `conda`
- Added the correct kernels:
``` bash 
sudo jupyter kernelspec install /Users/othmanerifki/opt/miniconda3/share/jupyter/kernels/xcpp11 --sys-prefix 
sudo jupyter kernelspec install /Users/othmanerifki/opt/miniconda3/share/jupyter/kernels/xcpp14 --sys-prefix 
sudo jupyter kernelspec install /Users/othmanerifki/opt/miniconda3/share/jupyter/kernels/xcpp17 --sys-prefix 
```

---

# Jupyter installation with Java 

Java kernel was easier.

- Install the Java Devleopment Kit (JDK) from https://www.oracle.com/java/technologies/javase-jdk14-downloads.html
- Then do: 

``` bash 
git clone https://github.com/SpencerPark/IJava.git
cd IJava/
./gradlew installKernel
```