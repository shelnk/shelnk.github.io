---
layout: post
title: "docker配置"
description: ""
category: dev
tags: []
modify: 2020-06-16 15:09:13
---


# windows mysql 5.7挂载配置文件
docker run -itd --name mysql -p 3306:3306 -v c:\tool\docker_v\mysql\conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
需要注意权限问题。设置file sharing 添加目录

-v /data/mysql/data:/var/lib/mysql

# mongo
$ docker run -itd --name mongo -p 27017:27017 mongo:4.2.8 --auth
$ docker exec -it mongo mongo admin
### 创建一个名为 admin，密码为 123456 的用户。
>  db.createUser({ user:'admin',pwd:'123456',roles:[ { role:'userAdminAnyDatabase', db: 'admin'}]});
### 尝试使用上面创建的用户信息进行连接。
> db.auth('admin', '123456')


docker run -itd --name redis-test -p 6379:6379 redis

# portainer

$ docker volume create portainer_data
$ docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer

-v /var/run/docker.sock:/var/run/docker.sock 
仅LINUX环境 

-v \.\pipe\docker_engine:\.\pipe\docker_engine \
仅Windosw环境 

docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer

#  es
 docker pull docker.elastic.co/elasticsearch/elasticsearch:6.8.9

 docker run -p 9200:9200 -p 9300:9300  -e ES_JAVA_OPTS="-Xms256m -Xmx256m" -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:6.8.9

# mariadb

docker run --name mariadb -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456  -d mariadb:5.5.64-trusty

# xxl-job-admin

docker run -e PARAMS="--spring.datasource.url=jdbc:mysql://192.168.31.69:3306/xxl_job?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&serverTimezone=Asia/Shanghai --spring.datasource.username=root --spring.datasource.password=123456" -p 9090:8080 --link mariadb:mariadb --name xxl-job-admin  -d xuxueli/xxl-job-admin:2.2.0

# 查看容器IP
docker exec -it  容器名/容器id ip addr




