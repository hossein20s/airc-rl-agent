AI RC Car RL Agent
===

Overview

This software is able to Self learning your AI RC Car 
by Deep reinforcement learning in few min.


## Description

AI RC Car like JetBot or JetRacer, DonkeyCar are  learning by supervised-learning.
supervised-learning needs much labeled data that written human. The behaivior quality 
is determined that data. Running behavior characteristic is determined that data.

Deep reinforcement learning (DRL) is can earned running behavior automatically through interaction with environment.
Do not need sample data that is human labelling.

This is using Soft Actor Critic as DRL algorithm. The algorithm is State of The Art of DRL in real environment.
In addition, using Variational Auto Encoder(VAE) as State representation learning. 
VAE can compress environment information, can speed up learning.

* This method devised by Arrafin
    * [Arrafine's Medium blog post](https://towardsdatascience.com/learning-to-drive-smoothly-in-minutes-450a7cdb35f4)
    * [Arrafine's implementsation for Simulator](https://github.com/araffin/learning-to-drive-in-5-minutes)


* About Soft actor critic
    * [Google AI blog Soft Actor-Critic: Deep Reinforcement Learning for Robotics](https://ai.googleblog.com/2019/01/soft-actor-critic-deep-reinforcement.html)

## Demo

This video is 
JetBot is learning running behavior on road in under 30 min. Software is running on Jetson Nano.  

[![](https://img.youtube.com/vi/j8rSWvcO-s4/0.jpg)](https://www.youtube.com/watch?v=j8rSWvcO-s4)


## Setup

### Requirements

* JetBot or JetRacer base image(Recommend latest images)
* tensorflow-gpu
* torch
* torchvision
* OpenCV

### Install

Dependency library install.

#### posix_ipc

```shell
sudo pip3 install posix_ipc
```

#### OpenAIGym 0.10.9

```
sudo apt install -y liblapack-dev scipy
sudo pip3 install gym==0.10.9
```

#### stable-baselines v2.9.0

```
$ sudo pip3 install -U Cython
$ cd ~/ && git clone https://github.com/hill-a/stable-baselines.git -b v2.9.0
# Before install, check below two comment.
$ cd stable-baselines/ && sudo python3 setup.py install

Install takes time.
```

1. Must be change setup.py. delete opencv-python from dependencies.

2. Must be change source code. line 433 in stable_baselines/sac/sac.py

* Current

```python
if step % self.train_freq == 0:
```

* TOBE

```python
if step % self.train_freq == 0 and done
```



#### clone this repository

```
$ cd ~/ && git clone https://github.com/masato-ka/airc-rl-agent.git
$ cd airc-rl-agent
```



## Usage

### Create VAE Model

1. Collect Environment data using ```jetbot_data_collection.ipynb``` . Image is 1k to 10k.
If you use on JetRacer, Using ```jetracer_data_collection.ipynb``` .
2. Leaning VAE using ```VAE_CNN.ipynb``` on other host machine such as Google Colaboratory.
3. Download vae.torch from host machine and deploy to root directory.

### Check and Evaluation 


Run ```notebooks/util/jetbot_vae_viewer.ipynb``` and Check reconstruction image.
Check that the image is reconstructed at several places on the course.

If you use on JetRacer, Using ```jetracer_vae_viewer.ipynb``` .

### Start learning

1. Run zmq_client.ipynb (needs game controller).
2. Run train.py

```shell
$ python3 train.py -robot jetbot
# If you use on JetRacer, "-robot jetracer". default is jetbot.
```

After few min, the AI car starts running. Please push STOP button immediately before the course out. 
And after, push START button. Repeat this.



## Contribution

* If you find bug or want to new functions, Please write issue.
* If you fix your self, please fork and send pull request.

## LICENSE

This software license under [MIT](https://github.com/masato-ka/airc-rl-agent/blob/master/LICENCE) licence.

## Author

[masato-ka](https://github.com/masato-ka)
