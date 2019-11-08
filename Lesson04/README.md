指定执行的进程
============

## 知识点

* 使用 ENTRYPOINT 指令指定执行的进程

## 实战演习

~~~bash
# 取得最新版的node.js镜像
$ sudo docker pull node:latest
# 启动容器，执行容器内命令
$ sudo docker container run node:latest ls /etc/
$ sudo docker container run node:latest cat /etc/hosts
$ sudo docker container run node:latest cat /etc/os-release
# 执行node进程，显示版本号
$ sudo docker image ls
$ sudo docker container run node:latest node -v
# 设置node为默认的进程，然后显示版本号
$ nano Dockerfile
...
FROM node:latest

ENTRYPOINT ["node"]
CMD [""]
...
$ sudo docker image build -t mynode:latest .
$ sudo docker image ls
$ sudo docker container run mynode:latest -v
$ sudo docker container run mynode:latest -help
# 使用CMD命令指定进程的默认参数
$ nano Dockerfile
...
FROM node:latest

ENTRYPOINT ["node"]
CMD ["-v"]
...
$ sudo docker image build -t mynode:latest .
# 显示版本号
$ sudo docker container run -it mynode:latest
# 显示帮助
$ sudo docker container run -it mynode:latest -help
# 评价执行js脚本
$ sudo docker container run -it mynode:latest -e "console.log('helo')"
~~~

## 课程文件

https://gitee.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
