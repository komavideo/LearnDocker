别问，问就先干
============

## 知识点

Docker使用主流程，本期以干货操作为主，内容比较多，具体说明请看下集。

* 建立Docker Image
* 编写应用程序
* 上推GitHub
* DockerHub云编译打包
* 下载使用Docker Image

## 实战演习

建立一个Docker版的Node.js应用，完成部署与分享。

### 应用技术

+ Node.js
+ Git
+ Github
+ Docker
+ Docker Hub

### 电脑1

~~~bash
# 建立Git库 -> https://github.com/komavideo

# 将Git库取得到本地
$ git clone https://github.com/komavideo/mynode
$ cd mynode
# 取得一个Node.js 8.16.1 LTS的镜像
$ sudo docker image pull node:8.16.1
$ sudo docker image ls
# 编写一个node.js的应用
$ nano helo.js
...
console.log("I love this game.")
...
# 要运行这个应用，首先建立一个Node.js的运行环境(container/容器)
$ nano Dockerfile
...
FROM node:8.16.1

RUN mkdir /src

COPY helo.js /src

CMD ["node", "/src/helo.js"]
...
# 编译打包我们的运行环境
$ sudo docker image build -t komavideo/mynode:v01 .
$ sudo docker image ls
# 在环境中运行我们的应用
$ sudo docker container run komavideo/mynode:v01

# Git提交
$ git add .
$ git commit -m "mynode1"
$ git push
$ git tag v01
$ git tag
$ git push origin v01

# Docker Hub云编译 -> https://hub.docker.com/
# Are you OK?

# Done.
~~~

### 电脑2

~~~bash
# 取得运行环境，运行应用
$ sudo docker image pull komavideo/mynode:latest
$ sudo docker container run komavideo/mynode:latest
$ sudo docker image pull komavideo/mynode:v01
$ sudo docker container run komavideo/mynode:v01
~~~

## 课程文件

https://gitee.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
