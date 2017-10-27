---
layout: single
title: 'Getting Started with Deep Learning'
category: tutorial
tags: [python, deep, learning, tensorflow, keras ]
comments: true
---

Getting ready for deep learning is not as hard as you might think. 

<center><img src = "https://static.wixstatic.com/media/4cd7bf_510a651475a449dcb9eb155537eff38f~mv2.png/v1/fill/w_630,h_366,al_c,usm_0.66_1.00_0.01/4cd7bf_510a651475a449dcb9eb155537eff38f~mv2.png"></center> 

Today, in this post, we will go through a simply tutorial to get started with deep learning on your pc/ laptop. Many people are freaked out at the initial set up process. It is not as complex as you think so, 
let us get on to it! At the end of this post, you will be able to install tensorflow with keras backend on your laptop and you will be able to start running some deep learning models like a scientist! 

<center><img src = "https://pm1.narvii.com/6444/077b1161a0cc5f63905da24884d70a0ce6e6b2ba_hq.jpg"></center>
_<center>what i feel when i think of deep learning</center>_ 

I will assume you have [anaconda3](https://www.anaconda.com/download/) enviroment installed, because it is really the best environment when it comes to doing data science using python. 

Also, make sure you have a pretty decent Nvidia graphics card if you are using laptop. (although this pretty much applies to desktop) Personally, I use a gaming laptop for doing much of my data science work.  

With that, let us begin. 

1. There will be 2 prerequisite to be able to run deep learning. We need to have **CUDA Toolkit 8.0** as well as **cuDNN v5.1 for CUDA 8.0**. As for now, you have to exact version of the 2 programs. 

<center><img src = "/image/"></center> 

we will get cuDNN v5.1[here](https://developer.nvidia.com/rdp/cudnn-download) as well as cuda 8.0 under the arhieves [here](https://developer.nvidia.com/cuda-toolkit-archive)

2. Once you have downloaded them. Install CUDA 8.0. I believe at the point where I was installing, they also required me to install microsoft visual studios. If during installation, you were prompt, then go ahead and [install MVS](https://www.visualstudio.com/downloads/) then return to install Cuda. (I downloaded the community version) 

3. Now, place your entire cuDNN file (unzipped) into your C: directory. Once that is done, you will have to add this to the environement path. 

```Command Prompt
C:\cudnn-8.0-windows10-x64-v5.1\cuda\bin
```

If you do not understand about environmental path, what you need to do is: Right click my computer > advanced system settings > environmental variables. You will see system variables. Scroll to this PATH variable and add the above line into it.

4. Create a new python environment soley for this. To do so, open **anaconda prompt** and type this:

```Command Prompt
conda create -n deeplearning python=3.5 numpy scipy matplotlib spyder ipython notebook
```
You can replace `deeplearning` with any name you want to. deeplearning is the name of the new python environment you will be creating. 

5. Once done, you must activate this environment. In future, if you want to do your deep learning, you must first activate this environment before proceeding: 

```Command Prompt
activate deeplearning
```

Then with deeplearning environment activated, 

```Command Prompt
pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/windows/gpu/tensorflow_gpu-1.0.1-cp35-cp35m-win_amd64.whl
```

Once it is done, continue to install keras: 

```Command Prompt
pip install keras
```

6. At this point, you are done! [Download this](https://github.com/antoniosehk/keras-tensorflow-windows-installation/blob/master/examples/mnist_mlp.py) sample py file and run it. It should take few minutes, indicating everything is done correctly. 

To run the file, again, go to anaconda prompt, 

```
activate deeplearning
python mnist_mlp.py
```

```

```

