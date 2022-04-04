---
title: docker使用
date: 2022-04-04 20:53:43
tags:
---

1.使用Dockerfile创建镜像

新建Dockerfile

输入

FROM centos:7

ADD index.html index.html #复制文件

生成镜像

docker build -t nginx . #最后加点表示当前目录

dokcer image ls

运行镜像容器

dokcer run -d -i –name cotainer nginx

进入容器

docker exec -it container bash

退出容器

exit

查看运行中容器

docker ps -a

查看镜像

docker image ls
