Docker Compose的基本使用
=======================

## 知识点

* Docker Compose的安装与使用

## 官网

https://docs.docker.com/compose/

## GitHub

https://github.com/docker/compose

## 实战演习

~~~bash
# 安装版本：https://github.com/docker/compose/releases
$ sudo curl -L https://github.com/docker/compose/releases/download/1.26.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ sudo docker-compose --version
# 卸载方法
$ sudo rm /usr/local/bin/docker-compose
~~~

### 开发Python Web应用(Flask)

```python
# main.py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return '你好! 吃饭了吗？'

if __name__ == "__main__":
    app.run(host="0.0.0.0", debug=True, port=5000)
```

### requirements.txt

```
flask==1.1.2
```

### Dockerfile

```bash
# 使用python3.8 alpine模板
FROM python:3.8.3-alpine3.12
# 将当前目录映射到容器内/app目录
ADD . /app
# 设置/app为工作目录
WORKDIR /app
# 安装python依赖包
RUN pip install -r requirements.txt
# 启动flask应用服务
CMD python main.py
```

### 命令操作

```bash
# 打包flask服务镜像
$ sudo docker build -t komavideo/myweb:0.1 .
$ sudo docker image ls
$ sudo docker container run --name myweb -d -p 8088:5000 komavideo/myweb:0.1
$ sudo docker container ls
$ curl http://127.0.0.1:8088
# 删除不用的容器
$ sudo docker container prune
```

### docker-compose.yml

*文件版本*  
https://docs.docker.com/compose/compose-file/

```yml
version: '3.8'
services:
  myweb:
    build: .
    ports:
    - "8088:5000"
    volumes:
    - .:/app
```

### 命令操作

```bash
# 容器启动
$ sudo docker-compose up
# 容器重新编译后启动
$ sudo docker-compose up --build
# 容器启动(精灵线程)
$ sudo docker-compose up -d --build
# 查询容器状态
$ sudo docker-compose ps
# 执行myweb容器内的命令
$ sudo docker-compose run myweb top
# 查看容器输出日志
$ sudo docker-compose logs -f myweb
$ sudo docker logs -f work_myweb_1
# 容器停止
$ sudo docker-compose stop
# 容器停止+消除(容器+网络)
$ sudo docker-compose down
# 容器停止+消除(容器+网络+镜像)
$ sudo docker-compose down --rmi all
```

## 课程文件

https://github.com/komavideo/LearnDocker

## 小马视频频道

http://komavideo.com
