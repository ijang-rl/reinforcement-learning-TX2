# Reinforcement Learning in TX2
July 4, 2018

## Step 1. Flash an OS and components
NVIDIA Jetson TX2 is flashed by JetPack 3.1 which includes:
* L4T 28.1 (which is an Ubuntu 16.04 64-bit variant(aarch64))
* CUDA 8.0
* cuDNN 6.0
* TensorRT 2.1
* openCV for Tegra 2.4

JetPack 3.1 is available here: 
  https://developer.nvidia.com/embedded/jetpack-3_1
  
JetPack installation guide is available here: 
  https://developer.nvidia.com/embedded/dlc/l4t-27-1-jetson-tx2-user-guide

## Step 2. Install TensorFlow
To install TensorFlow in TX2, we can followe [installTensorFlowTx2 by JetsonHacks](https://github.com/jetsonhacks/installTensorFlowTX2).

### Change the performance mode of TX2
```
$ sudo nvpmodel -m 2
```
About NVPmodel: https://www.jetsonhacks.com/2017/03/25/nvpmodel-nvidia-jetson-tx2-development-kit/

### Git clone
```
$ git clone https://github.com/jetsonhacks/installTensorFlowTX2
```

### Create a swapfile
```
$ cd installTensorFlowTX2
$ ./createSwapfile.sh -d ~/ -s 8
```

### Install dependencies for Python 2.7
```
$ ./installPrerequisites.sh
$ ./cloneTensorFlow.sh
$ ./setTensorFlowEV.sh
```

The followings are installed and cloned:
* Bazel 0.10.0
* TensorFlow 1.3

### Build TensorFlow
```
$ 
```
