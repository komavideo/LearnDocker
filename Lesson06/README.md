搭建Python的环境
===============

## 知识点

* 搭建Python的开发环境(Docker Hub)

## 实战演习

~~~bash
# 找到您需要使用的Python镜像，并下载到本地
$ sudo docker pull python:3.8.0-alpine3.10
$ sudo docker image ls
# 进入Python交互终端
$ sudo docker container run --rm -it python:3.8.0-alpine3.10
>>> help()
help> quit
>>> exit()
# Python和Pip版本确认
$ sudo docker container run --rm -it python:3.8.0-alpine3.10 python -V
$ sudo docker container run --rm -it python:3.8.0-alpine3.10 pip -V
# Linux版本确认
$ sudo docker container run --rm -it python:3.8.0-alpine3.10 cat /etc/os-release

################################################
# 执行本地的Python应用
$ nano main.py
...
import numpy as np
myarray = np.array([1,2,3,4,5])
print(myarray)
...
$ sudo docker container run --rm -it \
    -v /home/lcadmin/tmp:/workfolder:ro \
    python:3.8.0-alpine3.10 \
    python /workfolder/main.py

################################################
# 建立Python自己的镜像
$ nano Dockerfile
...
# alpine为musl libc核心，虽然小巧，但一部分功能受限，下面的numpy安装时需要UnixCCompiler编译才可通过
#FROM python:3.8.0-alpine3.10
FROM python:3.8

RUN pip3 install numpy
RUN mkdir -p /workfolder
COPY ./main.py /workfolder/

CMD [ "python", "/workfolder/main.py" ]
...
# 建立Python应用镜像
$ sudo docker image build -t goodpython:v01 .
$ sudo docker image ls
# 容器应用程序运行
$ sudo docker container run --rm -it goodpython:v01

################################################
# 代码管理对象(SVN/Git等)
+ Dockerfile
+ main.py

这样的话，开发团队只需要管理源代码文件和Dockerfile，而不用去关心开发环境的具体设置，确实方便。
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
