使用pgadmin4管理PostgreSql服务器
==============================

## 知识点

* pgadmin4 Docker镜像的基本使用(postgre数据库管理工具)

## 官网

https://www.pgadmin.org/

## Docker Hub

https://hub.docker.com/r/dpage/pgadmin4

## 实战演习

~~~bash
# 安装
$ sudo docker pull dpage/pgadmin4:4.16
$ sudo docker image ls
# 启动数据库服务
$ sudo docker pull postgres:9.6.16-alpine
$ sudo docker volume create --name v_webdb_data
$ sudo docker run --name webdb -v v_webdb_data:/var/lib/postgresql/data -p 5432:5432 -e POSTGRES_USER=dbuser -e POSTGRES_PASSWORD=12345678 -d postgres:9.6.16-alpine
# 启动pgadmin4服务
$ sudo docker run --name pgadmin4 -p 8080:80 \
    -e 'PGADMIN_DEFAULT_EMAIL=admin@komavideo.com' \
    -e 'PGADMIN_DEFAULT_PASSWORD=12345678' \
    -d dpage/pgadmin4:4.16
$ sudo docker container ls
# 停止Docker容器
$ sudo docker stop pgadmin4
$ sudo docker start pgadmin4
$ sudo docker stop webdb
# 显示系统内容器
$ sudo docker container ls -a
# 显示运行中容器
$ sudo docker container ls
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
