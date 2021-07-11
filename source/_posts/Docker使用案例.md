---
title: Docker使用案例
author: bucaike
top: false
cover: true
toc: true
mathjax: false
date: 2021-05-08 14:06:48
img: https://i.loli.net/2021/05/08/jiyugDbYdEJMQoA.png
coverImg: https://i.loli.net/2021/07/11/dZysXS9wqjKPJCL.png
summary: 这里介绍了几个Docker使用的案例，包括使用Docker和Docker-compose安装Owncloud，使用Docker安装WordPress等。你可以学到部署和控制容器。
tags:
  - Docker
  - Owncloud
categories:
  - 技术
---

# Docker使用案例

> 来自: 布菜克先生

## 安装Docker CE

[官方文档](https://docs.docker.com/v17.09/engine/installation/linux/docker-ce/ubuntu/)

## 使用Docker来安装OwnCloud

参见：[简书](https://www.jianshu.com/p/f09194ff94d5)

#### 直接安装

1.  拉取OwnCloud的官方docker镜像

    ```bash
    docker pull owncloud
    ```

    需要用root用户拉取，否则会有警告：

    ```csharp
    Warning: failed to get default registry endpoint from daemon (Cannot connect to the Docker daemon. Is the docker daemon running on this host?). Using system default: https://index.docker.io/v1/
    Cannot connect to the Docker daemon. Is the docker daemon running on this host?
    ```

2.  改用MySQL数据库

    `owncloud` 默认使用 `SQLite` 数据库，官方建议选择另外一个不同的数据库，特别当使用桌面客户端同步文件时，不鼓励使用 `SQLite`。

    拉取 `mysql` 官方docker镜像

    ```bash
    docker pull mysql
    ```

    启动 MySQL 容器，用作 owncloud 容器的数据库。

    ```bash
    docker run --name my-mysql -p 3306:3306 -v /var/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD="123456" -d mysql
    ```

    这里的密码为123456，端口是默认的`3306`，也可以用 `-p 宿主机映射端口:容器运行端口`来指定

3.  启动 owncloud 容器

    ```bash
    docker run --name owncloud -p 5679:80   -v /data/db/owncloud:/var/www/html/data --link my-mysql:mysql -d owncloud
    ```

    `-p 5679:80` 将容器的80端口映射到宿主局的5679端口。

    `--link my-mysql:mysql` ：将 `owncloud容器(客户)` 链接到 `my-mysql容器(服务)`，链接别名：`mysql`。

4.  配置 nginx 反向代理

    在 `etc/nginx/nginx.conf` 的 `http{}` 段写入:

    ```php
    upstream pan_server{
        server  127.0.0.1:5679;
    }
    
    server {
        listen   80;
        server_name pan.xxx.com;
        access_log /data/logs/nginx/pan.xxx.com.access.log;
        error_log /data/logs/nginx/pan.xxx.com.error.log;
    
        proxy_set_header X-Forwarded-For $remote_addr;
    
        location / {
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            add_header Cache-Control  "no-cache";
        
            proxy_pass http://pan_server;
            limit_rate 256m;
            client_max_body_size 0;
        }
    }
    ```

5. 安装 `owncloud`

   在浏览器上访问 `pan.xxx.com`，进入 owncloud 安装步骤：

   <img src="https://i.loli.net/2021/05/08/F2KdDVZO3H9cY5n.png" alt="安装步骤" style="zoom: 50%;" />

   这里可能会报错误：

   ```c
   SQLSTATE[HY000] [2054] The server requested authentication method unknown to the client
   ```

   原因是：

   MySQL 8默认使用了新的密码验证插件：`caching_sha2_password`，而之前的PHP版本中所带的mysqlnd无法支持这种验证

   解决方法两种，一种是升级PHP支持mysql8的新验证插件，另一种mysql验证方式降级。

   * 方法一

     先进入容器终端

     ```bash
     docker exec -it mysql /bin/bash
     ```

     默认是没有 vi的，先装它：

     ```bash
     apt update && apt install vim
     ```

     然后，mysql 配置文件 my.cnf添加配置：

     ```bash
     default_authentication_plugin=mysql_native_password
     ```

   * 方法二

     进入容器终端

     ```bash
     docker exec -it mysql /bin/bash
     ```

     在mysql下运行命令

     ```mysql
     ALTER USER 'YOURUSERNAME'@'%' IDENTIFIED WITH mysql_native_password BY 'YOURPASSWORD';
     ```

6. MySQL数据库配置：

   >   数据库用户：root
   >   数据库密码：123456
   >   数据库名：owncloud
   >   数据库主机：mysql 或 my-mysql

#### docker-compose安装

以将上面启动 owncloud 和 mysql 容器的两个步骤合成一步完成，这里介绍 `docker-compose` 的使用。

1.  安装

    ```bash
    pip install -U docker-compose
    ```

2.  docker-compose.yml 文件编写

    ```yml
    version: '2'
    services:
      owncloud:
        image: owncloud
        links: 
          - mysql:mysql
        volumes:
          - "/data/db/owncloud:/var/www/html/data"
        ports:
          - 5679:80
      mysql:
        image: mysql
        volumes:
          - "/data/db/mysql:/var/lib/mysql"
        ports:
          - 3306:3306
        environment:
          MYSQL_ROOT_PASSWORD: "123456"
          MYSQL_DATABASE: ownCloud
    ```

3.  docker-compose 运行和停止

    注意：`docker-compose` 必须在 `docker-compose.yml` 文件所在目录中执行，否则会报错

    docker-compose 后台启动

    ```bash
    docker-compose up -d
    ```

    docker-compose 查看状态

    ```bash
    # docker-compose ps
    ```

    docker-compose 停止和删除

    ```bash
    # docker-compose stop
    # dcoker-compose rm
    
    相当上面两条命令
    # dcoker-compose down
    ```

## 使用Dockera安装WordPress

1.  pull WordPress镜像

    ```bash
    sudo docker pull wordpress
    ```

2.  运行MySQL

    ```bash
    docker run -p 3306:3306 --name mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql
    ```

3.  创建WordPress数据库

    进入容器终端

    ```bash
    docker exec -it mysql /bin/bash
    ```

    进入mysql

    ```bash
    mysql -u root -p 123456
    ```

    创建数据库

    ```sql
    create database wordpress
    ```

4.  运行WordPress

    ```bash
    sudo docker run --name wordpress --link mysql:mysql -p 80:80 -d wordpress
    ```

    其中别名，主机端口号根据情况自行配置

5.  浏览器访问即可
