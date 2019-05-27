# Multiagent Reinforcement Learning in Nvidia TX2
July 4, 2018





## Step 1. Flash an OS and components

### Flash the L4T and components
NVIDIA Jetson TX2 can be flashed by JetPack 3.1 which includes:
* L4T 28.1 (which is an Ubuntu 16.04 64-bit variant(aarch64))
* CUDA 8.0
* cuDNN 6.0
* TensorRT 2.1
* openCV for Tegra 2.4

JetPack 3.1 is available here: 
  https://developer.nvidia.com/embedded/jetpack-3_1
  
JetPack installation guide is available here: 
  https://developer.nvidia.com/embedded/dlc/l4t-27-1-jetson-tx2-user-guide
    
### Add a swap file
TX2 uses a 8G unified memory which is shared between the CPU and GPU. When a model is trained, `OUT_OF_MEMORY` problems may occur. So we add some swap memory for TX2 as follows:
```
$ cd ~
$ fallocate -l 8G swapfile        # Create a 8G swapfile
$ chmod 600 swapfile              # Change permissions
$ ls -lh swapfile                 # List out the file
$ mkswap swapfile                 # Set up the Linux swap area
$ sudo swapon swapfile            # Now start using the swapfile
$ swapon -s                       # Show that it's now being used
```
How to add and delete swap space in Ubuntu: see [here](https://linuxize.com/post/how-to-add-swap-space-on-ubuntu-18-04/).

Swap memory in TX2 with a SSD: see [here](http://blog.naver.com/PostView.nhn?blogId=kangdonghyun&logNo=221046775377&categoryNo=17&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=search).

### Change the performance mode of TX2
```
$ sudo nvpmodel -m 0             # 0 means the best performance mode
```
About NVPmodel: https://www.jetsonhacks.com/2017/03/25/nvpmodel-nvidia-jetson-tx2-development-kit/
  




## Step 2. Install TensorFlow
To install TensorFlow in TX2, we can follow [this installation guide](https://docs.nvidia.com/deeplearning/frameworks/pdf/Install-TensorFlow-For-Jetson-TX2.pdf).

```
$ pip install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp33 tensorflow-gpu
```
TF installation for other Python + JetPack combinations: see [here](https://devtalk.nvidia.com/default/topic/1038957/jetson-tx2/tensorflow-for-jetson-tx2-/).


## Step 3. MAgent
Now, we will run the [MAgent](https://github.com/geek-ai/MAgent) (many-agent reinforcement learning) on TX2. The paper is shown here: https://arxiv.org/abs/1712.00600 

The baseline algorithms of MAgent are parameter-sharing DQN, DRQN, a2c in Tensorflow. DQN shows the best performance in large number sharing and gridworld settings.

### Git clone
```
$ git clone https://github.com/geek-ai/MAgent.git
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
> NOTE: You have to run following examples in the root of MAgent. DO NOT cd to `examples/`.
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

## Note
> MARL paper collection: https://github.com/LantaoYu/MARL-Papers

> RL Gitbook (in Korean): https://dnddnjs.gitbooks.io/rl/content/

> RL blog (by Jay Yang): https://jay.tech.blog/category/machine-learning/reinforcement-learning/
