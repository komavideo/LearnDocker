版本的选择与安装
==============

## 知识点

* Docker的版本
* Docker的安装

### Docker的版本

+ Docker Engine - Community
+ Docker Engine - Enterprise
+ Docker Enterprise

### Docker的安装

+ Docker Desktop for Windows
  - Windows 10 64-bit: Pro, Enterprise, or Education (Build 15063 or later).
  - 必须激活Windows平台特性：Hyper-V and Containers
  - 硬件需求：64位处理器，4G内存，BIOS虚拟化启用
+ Docker Desktop for Mac
  - 2010年后的Mac硬件
  - macOS为10.12以后
  - 4G内存
  - 与低版本的VirtualBox不兼容(>4.3.30)
+ Docker Engine - Community for Linux
  - CentOS
  - Fedora
  - Debian
  - Ubuntu
+ Docker Engine - Community for Ubuntu
  - Disco 19.04
  - Cosmic 18.10
  - Bionic 18.04.3 (LTS)
  - Xenial 16.04 (LTS)

## 实战演习

+ Ubuntu Server 18.04 LTS

https://docs.docker.com/install/linux/docker-ce/ubuntu/

~~~bash
# 系统更新
$ sudo apt update
$ sudo apt upgrade
$ sudo apt autoremove
# 安装系统依赖包
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
# 加入Docker信息库密钥
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88
# key确认
$ apt-key list
# 最后8位作为fingerprint参数
$ sudo apt-key fingerprint 0EBFCD88
# 将Docker信息库加入本地信息库当中
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
# 查看OS采用核心号
$ lsb_release -cs
# 查看信息库加入的位置和内容
$ cat /etc/apt/sources.list|grep docker

# 系统再更新
$ sudo apt update
$ sudo apt upgrade
# Docker安装
$ apt show docker-ce
$ sudo apt install docker-ce docker-ce-cli containerd.io
# 校验安装
$ docker help
$ docker version
$ sudo docker run hello-world
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
