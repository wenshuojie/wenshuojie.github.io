---
title: anaconda安装tensorflow-gpu
date: 2021-01-28
categories: tensorflow-gpu 环境配置
tags:
---
### anaconda安装tensorflow-gpu

#### 一 使用yml文件构建基础环境
文件名为<font color='red'>environment-windows.yml</font>  
不知道为什么pip:后声明了tensorflow-gpu但是我在安装完成之后并没有，所以后面才自己手动安装了tensorflow-gpu

```
name: tf2
channels:
  - conda-forge
  - defaults
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
dependencies:
  - graphviz
  - imageio=2.6.1
  - ipython=7.10.1
  - ipywidgets=7.5.1
  - joblib=0.14.0
  - jupyter=1.0.0
  - matplotlib=3.1.2
  - nbdime=1.1.0
  - nltk=3.4.5
  - numexpr=2.7.0
  - numpy=1.17.3
  - pandas=0.25.3
  - pillow=6.2.1
  - pip
  - py-xgboost=0.90
  - pydot=1.4.1
  - pyopengl=3.1.3b2
  - python=3.7
  - python-graphviz
  - requests=2.22.0
  - scikit-image=0.16.2
  - scikit-learn=0.22
  - scipy=1.3.1
  - tqdm=4.40.0
  - wheel
  - widgetsnbextension=3.5.1
  - pip:
    #- atari-py==0.2.6 # NOT ON WINDOWS YET
    - ftfy==5.7
    - gym==0.15.4
    - opencv-python==4.1.2.30
    - psutil==5.6.7
    - pyglet==1.3.2
    - spacy==2.2.4
    - tensorboard==2.1.1
    #- tensorflow-addons==0.8.3 # NOT ON WINDOWS YET
    #- tensorflow-data-validation==0.21.5 # NOT ON WINDOWS YET
    - tensorflow-datasets==2.1.0
    - tensorflow-estimator==2.1.0
    - tensorflow-hub==0.7.0
    #- tensorflow-metadata==0.21.1 # NOT ON WINDOWS YET
    #- tensorflow-model-analysis==0.21.6 # NOT ON WINDOWS YET
    - tensorflow-probability==0.9.0
    - tensorflow-serving-api-gpu==2.1.0 # or tensorflow-serving-api-gpu if gpu
    #- tensorflow-transform==0.21.2 # NOT ON WINDOWS YET
    - tensorflow-gpu==2.1.0 # or tensorflow-gpu if gpu
    - tf-agents==0.3.0
    #- tfx==0.21.2 # NOT ON WINDOWS YET
    - transformers==2.8.0
    - urlextract==0.13.0
    #- pyvirtualdisplay # add if on headless server

```
执行命令
```
conda env create -f environment-windows.yml
```
#### 二 手动安装tensorflow-gpu
由于在执行完yml文件并没有成功安装tensorflow-gpu  

1. 首先可以先修改conda源  
<font color='red'>清华源</font> 
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge 
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
#设置搜索时显示通道地址
conda config --set show_channel_urls yes
#pytorch的镜像
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
```
<font color='red'>查看源</font>
```
conda config --show channels
```
<font color='red'>移除源</font>
```
conda config --remove-key channels
```  

2. 执行安装命令
```
conda install tensorflow==2.1.0
```
在安装tensorflow 2.0以上版本时会自动安装上依赖的cuda(包名应该是cudatoolkit)和cudnn，省去了另外安装cuda和cudnn  

3. 检查是否安装成功
```
import tensorflow as tf
print('GPU',tf.test.is_gpu_available())
```
输出结果
![tensorflow-gpu安装成功](/assets/2021-01-28/01.png)