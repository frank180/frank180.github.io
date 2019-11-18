# 如何安装cuda和cudnn
这篇主要介绍如何在ubuntu18.04和ubuntu16.04上安装cuda和cudnn开发库，cuda和cudnn开发库是使用GPU进行人工智能训练必备的开发库

## 准备工作
 确认你Ubuntu没有安装了nvidia的驱动，如果安装的驱动不是41x的版本，使用下面的命令卸载
```bash
$ sudo apt remove nvidia*
$ sudo apt autoremove
```
## Ubuntu18.04

### 添加nvidia源码
```bash
$ wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.0.130-1_amd64.deb
$ sudo dpkg -i cuda-repo-ubuntu1804_10.0.130-1_amd64.deb
$ sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
$ sudo apt-get update
$ wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
$ sudo apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
$ sudo apt-get update

```

### 安装nvidia驱动
```bash
$ sudo apt-get install --no-install-recommends nvidia-driver-410
```
安装完毕，重启ubuntu，通过nvidia-smi命令确定是否安装成功
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 410.129      Driver Version: 410.129      CUDA Version: 10.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 108...  On   | 00000000:68:00.0  On |                  N/A |
| 52%   70C    P2   239W / 250W |   4565MiB / 11176MiB |     93%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1177      C   ./darknet                                   4187MiB |
|    0      1235      G   /usr/lib/xorg/Xorg                            17MiB |
|    0      1276      G   /usr/bin/gnome-shell                          13MiB |
|    0     16031      G   ...equest-channel-token=148587012417966454    54MiB |
|    0     27990      G   /usr/lib/xorg/Xorg                           146MiB |
|    0     28094      G   /usr/bin/gnome-shell                         141MiB |
+-----------------------------------------------------------------------------+

```
你的安装以后如果打印结果没有cuda是正常的，因为cuda还没有安装

### 安装cuda和cudnn
nvidia显卡驱动安装完以后就可以安装cuda和cudnn了
```bash
$ sudo apt-get install --no-install-recommends \
    cuda-10-0 \
    libcudnn7=7.6.2.24-1+cuda10.0  \
    libcudnn7-dev=7.6.2.24-1+cuda10.0
```
等待安装完成就可以了

## Ubuntu16.04

### 添加nvidia源
```bash
$sudo apt-get install gnupg-curl
$wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_10.0.130-1_amd64.deb
$sudo dpkg -i cuda-repo-ubuntu1604_10.0.130-1_amd64.deb
$sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
$sudo apt-get update
$wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64/nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb
$sudo apt install ./nvidia-machine-learning-repo-ubuntu1604_1.0.0-1_amd64.deb
$sudo apt-get update

```

### 安装nvidia驱动

```bash
$sudo mkdir /usr/lib/nvidia
$sudo apt-get install --no-install-recommends nvidia-driver-410
```
等待安装完毕，然后重启ubuntu系统，通过nvidia-smi系统查看安装是否成功
```bash
+-----------------------------------------------------------------------------+
 31 | NVIDIA-SMI 410.129      Driver Version: 410.129      CUDA Version: 10.0     |
 32 |-------------------------------+----------------------+----------------------+
 33 | GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
 34 | Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
 35 |===============================+======================+======================|
 36 |   0  GeForce GTX 108...  On   | 00000000:68:00.0  On |                  N/A |
 37 | 52%   70C    P2   239W / 250W |   4565MiB / 11176MiB |     93%      Default |
 38 +-------------------------------+----------------------+----------------------+
 39 
 40 +-----------------------------------------------------------------------------+
 41 | Processes:                                                       GPU Memory |
 42 |  GPU       PID   Type   Process name                             Usage      |
 43 |=============================================================================|
 44 |    0      1177      C   ./darknet                                   4187MiB |
 45 |    0      1235      G   /usr/lib/xorg/Xorg                            17MiB |
 46 |    0      1276      G   /usr/bin/gnome-shell                          13MiB |
 47 |    0     16031      G   ...equest-channel-token=148587012417966454    54MiB |
 48 |    0     27990      G   /usr/lib/xorg/Xorg                           146MiB |
 49 |    0     28094      G   /usr/bin/gnome-shell                         141MiB |
 50 +-----------------------------------------------------------------------------+

```
如果你的打印里没有cuda是正常的，cuda此时还没有安装

### 安装cuda和cudnn

```bash
$sudo apt-get install --no-install-recommends \
    cuda-10-0 \
    libcudnn7=7.6.2.24-1+cuda10.0  \
    libcudnn7-dev=7.6.2.24-1+cuda10.0
```
等待安装完成就可以了


## 通过nvidia官网deb包安装(备用)
使用repo的方法安装很容易因为网络问题卡住，或其他原因安装失败，失败的时候可以通过手动下载的方式安装

### 安装cuda

#### 下载cuda安装包
[点击这里进入cuda10.0下载界面](https://developer.nvidia.com/cuda-10.0-download-archive),按照下图选择，最后点击download按钮下载`cuda10.0`和`patch`。
![ubuntu0005-1](/images/ubuntu/ubuntu0005-1.jpg)

#### 安装cuda10.0

下载完毕以后，执行图中框框所示的shell命令(具体官方的命令为准)
```bash
$ sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-10.0.130-410.48_1.0-1_amd64.deb #18.04
$ sudo dpkg -i cuda-repo-ubuntu1604-10-0-local-10.0.130-410.48_1.0-1_amd64.deb #16.04
$ sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get install cuda
$ sudo dpkg -i cuda-repo-ubuntu1804-10-0-local-nvjpeg-update-1_1.0-1_amd64.deb #18.04
$ sudo dpkg -i cuda-repo-ubuntu1604-10-0-local-nvjpeg-update-1_1.0-1_amd64.deb #16.04
```

#### 验证安装是否成功

安装完成以后，重启ubuntu,使用命令`nvidia-smi`检查是否安装成功
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 410.129      Driver Version: 410.129      CUDA Version: 10.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 108...  On   | 00000000:68:00.0  On |                  N/A |
| 52%   71C    P2   125W / 250W |   4394MiB / 11176MiB |     93%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1177      C   ./darknet                                   4015MiB |
|    0      1235      G   /usr/lib/xorg/Xorg                            17MiB |
|    0      1276      G   /usr/bin/gnome-shell                          13MiB |
|    0     16031      G   ...equest-channel-token=148587012417966454    54MiB |
|    0     27990      G   /usr/lib/xorg/Xorg                           146MiB |
|    0     28094      G   /usr/bin/gnome-shell                         142MiB |
+-----------------------------------------------------------------------------+

```

### 安装cudnn

#### 下载cudnn
[点击这里进入nvdia的cudnn官网](https://developer.nvidia.com/rdp/form/cudnn-download-survey),然后注册一个nvdia开发者账号，登录以后，按照图示下载
![cudnn](/images/ubuntu/ubuntu0005-2.jpg)

#### 安装cudnn
```
$ sudo dpkg -i libcudnn7_7.6.4.38-1+cuda10.0_amd64.deb
$ sudo dpkg -i libcudnn7-dev_7.6.4.38-1+cuda10.0_amd64.deb
$ sudo dpkg -i libcudnn7-doc_7.6.4.38-1+cuda10.0_amd64.deb
```

## 配置cuda

### 添加相关

打开bash的配置文件

```bash
vim ~/.bashrc (或者 gedit ~/.bashrc)
```
在文件尾添加cuda相关配置

```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.0/lib64
export PATH=$PATH:/usr/local/cuda-10.0/bin
export CUDA_HOME=$CUDA_HOME:/usr/local/cuda-10.0
```
### 验证

重新加载配置文件
```bash
$ source ~/.bashrc
```

终端输入 `nvcc --version`,出现类似信息即是配置成功
```bash
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2018 NVIDIA Corporation
Built on Sat_Aug_25_21:08:01_CDT_2018
Cuda compilation tools, release 10.0, V10.0.130
```


## FAQ

#### 为什么安装cuda10.0
nvidia官网目前最新的版本是cuda10.1，cuda10.2也即将发布了，但是很多深度学习的平台，比如tensorflow,只支持cuda10.0，即使你成功安装了cuda10.1，在训练主流平台的模型时，会报一个GPU kernel的错误，这个错误产生的原因就是cuda不匹配造成的。

#### 为什么不能使用`ubuntu-drivers autoinstall`安装nvidia驱动
使用ubuntu自带的命令安装nvidia会安装库里最新的驱动。由于cuda10.1已经发布，ubuntu官方的库里默认安装的nvdia driver版本是43x。nvidia官网写明了，cuda10.1适配43x以上的驱动，10.1适配41x以上的驱动。因此在cuda选择了10.0以后，就不能再使用自动安装了，否则cuda与nvdia driver不匹配也会导致cuda报错。

#### 为什么安装nvidia-driver-410
可以选择`nvidia-driver-410`或者`nvidia-driver-418`,`nvidia-driver-410`是我的使用的版本，按照nvidia官方的说明，`nvidia-driver-410`和`nvidia-driver-418`均支持，并且在tensorflow官方文档中，推荐是安装`nvidia-driver-418`。

#### 关于`nvcc --version`未找到
1. 确认你是否使用了bash，如果你使用了其他shell，比如zsh，把配置cuda步骤的.bashrc文件替换成相应的配置文件
2. 确认你的cuda安装目录是否为`/usr/local/cuda-10.0`


