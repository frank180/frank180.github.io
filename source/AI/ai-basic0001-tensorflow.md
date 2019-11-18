# 如何安装配置TensorFlow开发环境
1. 这篇教程主要介绍如何在Ubuntu18.04上安装TensorFlow开发环境，其他开发环境请参照TensorFlow官方的说明，需要的依赖和本文基本相同。
2. 不使用虚拟环境可以跳过虚拟环境相关的步骤，示例使用python3，使用python2的替换pip工具即可。
3. 安装GPU版本的tensorflow，需要先安装好cuda和cudnn，可参考这里的方式安装:[配置和安装cuda&cudnn](/ubuntu/ubuntu0005-install-nvidia.html)

## 基础环境

### 更新系统安装基础工具

```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install build-essential git wget 
```

### python开发环境

```bash
$ sudo apt install python3-dev python3-pip
```

### 安装虚拟环境工具(推荐使用)

```bash
$ sudo pip3 install -U virtualenv 
```

## 虚拟环境创建和使用(不使用虚拟环境跳过这部分)
使用虚拟环境的好处是可以将tensorflow从主机中隔离出来，不会破坏主机的环境，同时安装好的环境不会被其他工具破坏。也可以安装多个版本的tensorflow

### 创建虚拟环境
```bash
$ virtualenv --system-site-packages -p python3 /path/to/venv
```
1. venv      :是你的虚拟环境的名字，建议按照安装的版本号命名，如：安装gpu1.14的版本，命令为venv-gpu-1.14.安装cpu.1.10版本，命令为venv-cpu.1.10
2. /path/to/ :是要安装的路径，一般安装在home目录下，即: ~/ 

### 如何使用虚拟环境

#### 进入虚拟环境
```bash
$ source /path/to/venv/bin/activate
```
进入虚拟环境后，终端会带上前缀`(venv)`.比如我的:
```bash
(venv-gpu-1.14) yan@yan-pc:~$
```

#### 退出虚拟环境
```
$ deactivate
```
退出后前缀消失了，就是正常退出了。

## 安装tensorflow和keras
1. 默认tensorflow会安装2.0的版本，安装tensorflow1.x的版本需要制定版本号
2. 依赖会自动安装，同时tensorboard等工具也会同时安装相应的版本

### TensorFlow2.0

#### 安装GPU版本
```bash
(venv)$ pip install --upgrade tensorflow-gpu     #使用虚拟环境
$ pip3 install --upgrade tensorflow-gpu          #直接使用python3安装
```
#### 安装CPU版本
```bash
(venv)$ pip install --upgrade tensorflow         #使用虚拟环境
$ pip3 install --upgrade tensorflow              #直接使用python3安装
```
### TensorFlow1.x
1.14是LTS版本，安装旧版本，直接指定需要的版本即可,这里以安装1.14为例

####　安装GPU版本
```bash
(venv)$ pip install  tensorflow-gpu==1.14         #使用虚拟环境
$ pip3 install --upgrade tensorflow-gpu==1.14     #直接使用python3安装
```
#### 安装CPU版本
```bash
(venv)$ pip install  tensorflow==1.14         #使用虚拟环境
 75 $ pip3 install  tensorflow==1.14 #直接使用python3安装
```
### 验证安装
```bash
$ python -c "import tensorflow as tf;print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
```
验证的时候你可能会看到很多的警告，这是正常的，只要未出现error，会在最后看到下列的代码，即是安装成功
```bash
Tensor("Sum:0", shape=(), dtype=float32)
```
### 安装keras
keras直接安装即可

```bash
(venv) $ pip install keras                        #使用虚拟环境
$ pip3 install keras                              #直接使用python3安装
```

## FAQ

#### 运行时出现kernel错误
安装GPU版本时，要先确认cuda和cudnn是否正常安装，可参考这里，[配置和安装cuda&cudnn](/ubuntu/ubuntu0005-install-nvidia.html)

#### 安装出现not found或者安装到一半报错
tensorflow源在国外，安装时下载会比较慢，出现这种错误直接重新安装命令就可以

#### 运行是出现model not found的错误
运行`pip list`查看已经安装的库列表，查看是否未安装，使用`pip install`安装相应的库就可以



