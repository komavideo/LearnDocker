搭建PostgreSql数据库服务器
========================

## 知识点

* 使用Docker镜像搭建PostgreSql数据库服务器

## 官网

https://hub.docker.com/_/postgres

### PostgreSql

https://www.postgresql.org/

*Versioning Policy*

https://www.postgresql.org/support/versioning/

## 实战演习

~~~bash
# 找到适合您的PostgreSql版本
$ sudo docker pull postgres:9.6.16-alpine
# 启动PostgreSql数据库服务器 - webdb
$ sudo docker run --name webdb -p 5432:5432 -e POSTGRES_USER=dbuser -e POSTGRES_PASSWORD=12345678 -d postgres:9.6.16-alpine
# 数据库容器(服务)查看
$ sudo docker container ls
$ nmap 127.0.0.1
# psql连接
$ psql -h localhost -U dbuser
Password for user dbuser:
dbuser=# select * from pg_tables;
dbuser=# \q

# 数据库服务停止
$ sudo docker stop webdb
$ nmap 127.0.0.1
$ sudo docker container ls
$ sudo docker container ls -a
# 数据库服务再开
$ sudo docker start webdb
# 进入数据库实例的bash
$ sudo docker exec -it webdb /bin/bash
bash-5.0# cd /var/lib/postgresql/data
bash-5.0# ls
bash-5.0# cat pg_hba.conf
bash-5.0# cat postgresql.conf
bash-5.0# exit

######################################
# 课题：数据库文件脱离Docker容器永久保存
######################################
# 建立专用的独立使用的卷(Volume)
$ sudo docker volume create --name v_webdb_data
$ sudo docker volume ls
$ sudo docker volume inspect v_webdb_data
# 清理旧的webdb实例
$ sudo docker stop webdb
$ sudo docker container rm webdb
$ sudo docker container ls -a
# 建立新的webdb实例
$ sudo docker run --name webdb -v v_webdb_data:/var/lib/postgresql/data -p 5432:5432 -e POSTGRES_USER=dbuser -e POSTGRES_PASSWORD=12345678 -d postgres:9.6.16-alpine
# 绑定卷的查看
$ sudo docker inspect webdb
...
        "Mounts": [
            {
                "Type": "volume",
                "Name": "v_webdb_data",
                "Source": "/var/lib/docker/volumes/v_webdb_data/_data",
                "Destination": "/var/lib/postgresql/data",
                "Driver": "local",
                "Mode": "z",
                "RW": true,
                "Propagation": ""
            }
        ],
...
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
