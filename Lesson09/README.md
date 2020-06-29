搭建你的缓存服务器Redis
====================

## 知识点

* 使用Docker技术搭建Redis服务器

## 官网

https://redis.io/

## Docker Hub

https://hub.docker.com/_/redis/

## 实战演习

~~~bash
# 安装
$ sudo docker pull redis:6.0.5-alpine
$ sudo docker image ls
# 建立Redis永久化卷标
$ sudo docker volume create --name v_redis_data
$ sudo docker volume ls
$ sudo docker run --name redis1 -v v_redis_data:/data -p 6379:6379 -d redis:6.0.5-alpine redis-server --appendonly yes --requirepass 12345678
$ sudo docker container ls
# 确认本地打开的tcp端口号
$ netstat -nltp
$ sudo docker exec -it redis1 top
# 启用客户端连接redis1服务
$ sudo apt install redis-tools
$ redis-cli -h 127.0.0.1 -p 6379 -a 12345678
127.0.0.1:6379> ping
127.0.0.1:6379> info
127.0.0.1:6379> set data01 "helo, redis."
127.0.0.1:6379> get data01
127.0.0.1:6379> set data02 "komavideo"
127.0.0.1:6379> get data02
127.0.0.1:6379> keys *
127.0.0.1:6379> exit
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
