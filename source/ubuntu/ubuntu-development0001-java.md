# Ubuntu下Java的安装和配置
ubuntu下Java有两种安装方式，一种是开源的Openjdk，一种是下载完整的JDK安装。


## Openjdk安装
Ubuntu的软件库里默认有一个Jdk。但是OpenJdk是开源版本，不具备完整功能，同时很多软件的编译都不能使用openjdk来编译。OpenJdk的安装方法如下
```bash
$ sudo apt update
$ sudo apt install openjdk-8-jdk
```
下载的是openjdk8的版本(也是默认版本)，通过`apt search`命令可以查看完整的jdk列表
```bash
$ sudo apt search openjdk
Sorting... Done
Full Text Search... Done
default-jdk/bionic-updates,bionic-security 2:1.11-68ubuntu1~18.04.1 amd64
  Standard Java or Java compatible Development Kit

default-jdk-doc/bionic-updates,bionic-security 2:1.11-68ubuntu1~18.04.1 amd64
  Standard Java or Java compatible Development Kit (documentation)

...

libreoffice/bionic-updates,bionic-security 1:6.0.7-0ubuntu0.18.04.10 amd64
  office productivity suite (metapackage)

openjdk-11-dbg/bionic-updates,bionic-security 11.0.4+11-1ubuntu2~18.04.3 amd64
  Java runtime based on OpenJDK (debugging symbols)

openjdk-11-demo/bionic-updates,bionic-security 11.0.4+11-1ubuntu2~18.04.3 amd64
  Java runtime based on OpenJDK (demos and examples)

openjdk-11-doc/bionic-updates,bionic-updates,bionic-security,bionic-security 11.0.4+11-1ubuntu2~18.04.3 all
  OpenJDK Development Kit (JDK) documentation

openjdk-8-jdk/bionic-updates,bionic-security 8u222-b10-1ubuntu1~18.04.1 amd64
  OpenJDK Development Kit (JDK)

openjdk-8-jdk-headless/bionic-updates,bionic-security 8u222-b10-1ubuntu1~18.04.1 amd64
  OpenJDK Development Kit (JDK) (headless)

openjdk-8-jre/bionic-updates,bionic-security 8u222-b10-1ubuntu1~18.04.1 amd64
  OpenJDK Java runtime, using Hotspot JIT

...
```
需要安装指定的版本可以直接指定安装，如:
```bash
$ sudo apt install openjdk-11-jdk
```

## Oracle Java
### Java下载
完整的代码包需要从[oracle Java的官网](https://www.oracle.com/technetwork/java/javase/downloads/index.html)下载,没有oracle账号的需要先注册一个。
这里以安装Java8的长期支持版本为例，选择java8版本，
![ubuntu-development0001-1](/images/ubuntu/ubuntu-development0001-1.jpg)
点击`Accept License Agreement`，同意后选择linux版本，64位的选择x64,32位的选择x86.这里以x64为例
![ubuntu-development0001-2](/images/ubuntu/ubuntu-development0001-2.jpg)

### Java安装

#### 解压
```bash
$ tar -zxvf jdk-8u221-linux-x64.tar.gz
```
#### 转移到系统目录
```bash
$ sudo mv jdk1.8.0_221/ /usr/local/
```

### Java配置
java放到系统目录以后，需要配置shell的配置文件才能正常使用。这里以bash为例,
编辑配置文件
```bash
$ vim ~/.bashrc
```
添加Java路径到文件末尾
```
export JAVA_HOME=/usr/local/jdk1.8.0_221/
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```
配置完了以后重启终端或者重新加载配置文件
```bash
$ source ~/.bashrc
```
### 验证
通过java命令查看版本号，正确安装和配置时查看的结果如下
```bash
$ java -version
java version "1.8.0_221"
Java(TM) SE Runtime Environment (build 1.8.0_221-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.221-b11, mixed mode)
```
