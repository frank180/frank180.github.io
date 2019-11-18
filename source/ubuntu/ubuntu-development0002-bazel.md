# 安装bazel在Ubuntu18.04上
bazel是一种类似make的代码编译工具，很多项目会使用bazel编译，比如TensorFlow的silm工具。

## 准备

### 依赖安装
```bash
# sudo apt install pkg-config zip g++ zlib1g-dev unzip python3
```
### 准备java环境
按照这个文档进行安装[安装java](/ubuntu/ubuntu-development0001-java.html)

## 获取安装的脚本

### 从github获取
这里以0.29.1为例，具体下载那个版本依据需求下载,下载linux_x64的sh文件
![ubuntu-development0002-1](/images/ubuntu/ubuntu-development0002-1.png)

### 添加执行的权限
```bash
chmod +x bazel-0.29.1-installer-linux-x86_64.sh
```

## 安装以及验证

### 安装

```bash
$ ./bazel-0.29.1-installer-linux-x86_64.sh --user
```
`--user`选项是可选的，加上`--user`选项会安装在HOME目录并将`.bazelrc`路径设置为`$HOME/.bazelrc`。加上的好处是其他用户可以安装版本和你不同的bazel工具。不同软件对bazel版本有不同的需求

### 配置(`--user`)
使用了`--user`选项以后，需要配置路径到shell的配置文件。
```bash
$ vim ~/.bashrc
```
在文件尾添加
```
export PATH="$PATH:$HOME/bin"
```
重启终端或者重新加载配置文件
```bash
$ source ~/.bashrc
```

### 验证
通过`bazel version`命令可以查看到版本号就是安装成功了
```
$ bazel version
WARNING: --batch mode is deprecated. Please instead explicitly shut down your Bazel server using the command "bazel shutdown".
Build label: 0.29.1
Build target: bazel-out/k8-opt/bin/src/main/java/com/google/devtools/build/lib/bazel/BazelServer_deploy.jar
Build time: Tue Sep 10 13:44:39 2019 (1568123079)
Build timestamp: 1568123079
Build timestamp as int: 1568123079
```

