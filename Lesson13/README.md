搭建React开发环境
===============

## 知识点

* 使用Node.js Docker镜像搭建Reast.js开发环境

## 官网

### Node.js Docker

https://hub.docker.com/_/node

### React.js

https://zh-hans.reactjs.org/

## 实战演习

~~~bash
$ cd work
$ mkdir app
$ nano Dockerfile
...
FROM node:12.18.2-alpine3.9
ADD ./app /app
WORKDIR /app
...
$ nano docker-compose.yml
...
version: '3.8'
services:
  node:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - ./app:/app
    command: sh -c "cd react-sample && yarn start"
    ports:
      - "3000:3000"
    stdin_open: true # 标准输入
...
# 编译前拉下docker node镜像
$ sudo docker pull node:12.18.2-alpine3.9
$ sudo docker image ls
# 编译容器服务
$ sudo docker-compose build
# 生成一个React应用程序
$ sudo docker-compose run --rm node sh -c "npm install -g create-react-app && create-react-app react-sample"
# 容器内确认生成的项目
$ sudo docker-compose run node ls
# 确认本地文件夹的app目录
$ ls ./app
# 启动容器
$ sudo docker-compose up
# 浏览器访问
>http://localhost:3000
$ nano app/react-sample/src/App.js
...
Helo React.js
...
~~~

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
