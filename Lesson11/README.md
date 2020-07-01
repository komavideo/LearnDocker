Flask+Redis多服务开发部署
=======================

## 知识点

* Docker Compose多服务开发部署(Flask, Redis)

## 服务结构设计

```
client <---> web(flask:myweb) <---> db(redis:myredis)
```

## 实战演习

### main.py

```python
from flask import Flask
from redis import Redis

app = Flask(__name__)
redis = Redis(host='myredis', port=6379)

@app.route('/')
def hello():
    redis.incr('hits')
    return '你好! 我们见过 %s 次面。' % redis.get('hits')

if __name__ == "__main__":
    app.run(host="0.0.0.0", debug=True, port=5000)
```

### requirements.txt

```
flask==1.1.2
redis==3.5.3
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
    depends_on:
    - myredis
  myredis:
    image: redis:6.0.5-alpine
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
# 确认本地打开的tcp端口号
$ netstat -nltp
# Web访问测试
$ curl http://127.0.0.1:8088
# 执行myweb容器内的命令
$ sudo docker-compose run myweb top
# 查看容器输出日志
$ sudo docker-compose logs -f
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
