搭建Vue开发环境
==============

## 知识点

* Docker Node.js镜像的使用
* 安装Vue Cli4等工具包

## 官网

https://hub.docker.com/_/node

## 实战演习

~~~bash
# Ubuntu镜像取得
$ sudo docker pull node:12.18.1-buster
$ sudo docker image ls
$ mkdir src
~~~

### Dockerfile

~~~bash
FROM node:12.18.1-buster
ADD ./src /app
WORKDIR /app
ENV DEBCONF_NOWARNINGS yes
RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y \
        build-essential -y \
        curl \
        nmap \
        git \
        nano \
    && rm -rf /var/lib/apt/lists/*
RUN npm install -g @vue/cli@4.4.6
~~~

### 命令操作

~~~bash
$ sudo docker image build -t koma/vuecli4:0.1 .
$ sudo docker image ls
$ sudo docker container run -it --name vuecli4 -v `pwd`/src:/app -p 8080:8080 -d koma/vuecli4:0.1
$ sudo docker container ls
$ sudo docker exec -it vuecli4 /bin/bash
root@5e6a97287da5:/app# vue -V
root@5e6a97287da5:/app# nano ~/.bashrc
...
export LS_OPTIONS='--color=auto'
alias ls='ls $LS_OPTIONS'
alias ll='ls $LS_OPTIONS -l'
alias l='ls $LS_OPTIONS -lA'
...
root@5e6a97287da5:/app# nano ~/.vuerc
...
{
  "useTaobaoRegistry": false,
  "packageManager": "yarn"
}
...
root@5e6a97287da5:/app# vue create myweb
root@5e6a97287da5:/app/myweb# cd myweb
root@5e6a97287da5:/app/myweb# npm run serve

# 通过本地8080端口访问vue应用程序
$ curl http://192.168.x.x:8080

Done.
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
