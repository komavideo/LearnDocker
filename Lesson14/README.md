Amazon Linux 2安装Docker
=======================

## 知识点

* 使用 AWS EC2 服务，在 Amazon Linux 2 上安装 Docker

## 官网

https://aws.amazon.com/cn/amazon-linux-2/

## 实战演习

~~~bash
# 确认 linux 系统版本
$ cat /etc/os-release
# 使用 amazon-linux 扩展包安装 docker
$ sudo amazon-linux-extras list
$ sudo amazon-linux-extras install -y docker
# 修改 docker 附加组给 ec2-user
$ sudo usermod -a -G docker ec2-user
$ docker version
# 启动 docker 服务
$ sudo systemctl start docker
# 确认 docker 运行
$ ps aux|grep docker
# 注册 docker 服务
$ sudo systemctl enable docker
# OS重新启动
# $ sudo reboot
################################################
# 下载 nginx web服务器
$ sudo docker pull nginx
$ sudo docker image ls
$ sudo docker container run --name myweb -d -p 80:80 -it --rm nginx
$ sudo docker container ls -a
$ curl http://127.0.0.1
$ sudo docker container stop myweb
$ sudo docker container ls -a
$ curl http://127.0.0.1
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com

## 小马部落

https://discord.gg/VSKw72P