---
title: "Setup a Deep Learning Server"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: "How to setup working locally with remote files"
type: technical_note
draft: false
---

### Basic of python installation
``` bash 
curl https://pyenv.run | bash
pyenv install --list
pyenv install 3.8.7
pyenv global 3.8.7
```

### Preliminaries
``` bash
sudo apt-get update
sudo apt-get install build-essential
sudo apt-get install -y build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev git
```
### SDK & Java
``` bash 
curl -s "https://get.sdkman.io" | bash
source "/home/othrif/.sdkman/bin/sdkman-init.sh"
sdk install java
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install sbt
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```


### Other packages

``` bash 
sudo apt-get install awscli
sudo apt-get install git
```

### Install CUDA, cuDNN, tensorflow
Check version compatibility in:
* https://www.tensorflow.org/install/source#gpu
* https://www.tensorflow.org/install/gpu#install_cuda_with_apt
* CUDA toolkit: https://developer.nvidia.com/cuda-toolkit 
* CUDNN: https://developer.nvidia.com/rdp/cudnn-archive

``` bash 
pip install tensorflow

sudo apt -y install build-essential
sudo apt -y install gcc-8 g++-8 gcc-9 g++-9

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8 --slave /usr/bin/g++ g++ /usr/bin/g++-8
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9 --slave /usr/bin/g++ g++ /usr/bin/g++-9

sudo update-alternatives --config gcc # select gcc-8 option (1)
gcc --version # to check it is gcc 8

# Get CUDA Toolkit
# TF 2.4.0 compatibel with cuDNN 8.0 and CUDA 11.0
wget https://developer.download.nvidia.com/compute/cuda/11.0.3/local_installers/cuda_11.0.3_450.51.06_linux.run
sudo bash cuda_11.0.3_450.51.06_linux.run # Deslect CUDA driver and install
# Add the following to the bashrc file
export PATH=$PATH:/usr/local/cuda-11.0/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.0/lib64

# Get cuDNN package
tar -xvf cudnn-11.0-linux-x64-v8.0.5.39.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
nvcc --version
nvidia-smi
python -c "import tensorflow as tf; tf.config.list_physical_devices('GPU')"
```

Run performance:
``` bash 
git clone https://github.com/tensorflow/benchmarks
python benchmarks/scripts/tf_cnn_benchmarks/tf_cnn_benchmarks.py --num_gpus=1 --model resnet50 --batch_size 64
```
compare with https://www.leadergpu.com/tensorflow_resnet50_benchmark