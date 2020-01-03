容器的使用
=========

## 知识点

* 寻找镜像(Docker Hub)
* 镜像的基本使用方法

## 实战演习

### Docker Hub

不要重复发明轮子，Docker Hub上应有尽有，您应该在准备自己建立镜像之前，先去Docker Hub上寻找现有的镜像模版，特别是官方认证的镜像。

### 镜像的使用

我们建立一个基于 Nginx 的Web服务器吧，自己管理维护的那种。

~~~bash
# 找到您需要使用的镜像，并下载到本地
$ sudo docker pull nginx:1.17.5-alpine
$ sudo docker image ls
# 列出容器内目录
$ sudo docker container run nginx:1.17.5-alpine ls
# 确认容器核心版本
$ sudo docker container run nginx:1.17.5-alpine cat /etc/os-release
# 列出nginx设置目录
$ sudo docker container run nginx:1.17.5-alpine ls -R -l /etc/nginx
# 查看nginx全局设置文件
$ sudo docker container run nginx:1.17.5-alpine cat /etc/nginx/nginx.conf
# 查看默认Web虚拟主机设置文件
$ sudo docker container run nginx:1.17.5-alpine cat /etc/nginx/conf.d/default.conf
# 确认虚拟目录下面的内容
$ sudo docker container run nginx:1.17.5-alpine ls -R -l /usr/share/nginx/html
# 启动容器，确认效果
$ sudo docker container run --name myweb -d -p 8088:80 nginx:1.17.5-alpine
$ sudo docker container ls
# 服务动作确认
$ curl http://127.0.0.1:8088
# 停止容器服务
$ sudo docker container stop myweb
# 启动存在的容器
$ sudo docker container start myweb
# 列出所有容器
$ sudo docker container ls -a
# 删除指定容器
$ sudo docker container rm -f myweb
# 删除所有容器
$ sudo docker container prune

#####################################
# 建立本地的Web目录和文件
#####################################
$ mkdir myweb
$ cd myweb
$ nano index.html
...
<h1>Helo Docker world.</h1>
...
$ sudo docker container run --name myweb -d -p 8088:80 -v /home/lcadmin/myweb:/usr/share/nginx/html:ro nginx:1.17.5-alpine
# 服务动作确认
$ curl http://127.0.0.1:8088
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
