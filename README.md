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
To install TensorFlow in TX2, we can follow [installTensorFlowTx2 by JetsonHacks](https://github.com/jetsonhacks/installTensorFlowTX2).

### Change the performance mode of TX2
```
$ sudo nvpmodel -m 2
```
About NVPmodel: https://www.jetsonhacks.com/2017/03/25/nvpmodel-nvidia-jetson-tx2-development-kit/

### Git clone
```
$ git clone https://github.com/jetsonhacks/installTensorFlowTX2
$ cd installTensorFlowTX2
```

### Create a swapfile
```
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

## Step 3. MAgent
Now, we will run the [MAgent](https://github.com/geek-ai/MAgent) (many-agent reinforcement learning) on TX2.
The paper is shown here: https://arxiv.org/abs/1712.00600

The baseline algorithms of MAgent are parameter-sharing DQN, DRQN, a2c in Tensorflow. 
DQN shows the best performance in large number sharing and gridworld settings.

### Git clone
```
$ git clone git@github.com:geek-ai/MAgent.git
$ cd MAgent
```

### Install dependencies
```
$ sudo apt-get install cmake libboost-system-dev libjsoncpp-dev libwebsocketpp-dev
```

### Build MAgent
```
$ bash build.sh
$ export PYTHONPATH=$(pwd)/python:$PYTHONPATH
```

### Run examples
#### Train
* pursuit
```
$ python examples/train_pursuit.py --train
```
* gathering
```
$ python examples/train_gather.py --train
```
* battle
```
$ python examples/train_battle.py --train
```
#### Play
* battle game
```
$ python examples/show_battle_game.py
```
