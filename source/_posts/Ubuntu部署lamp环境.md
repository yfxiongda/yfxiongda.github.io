---
title: Ubuntu部署lamp环境
author: bucaike
top: false
cover: false
toc: true
mathjax: false
date: 2021-05-08 14:23:25
img: https://i.loli.net/2021/05/08/GfvLj2Ubxpz6P47.png
coverImg: https://i.loli.net/2021/05/08/GfvLj2Ubxpz6P47.png
summary: 本文介绍了如何在Ubuntu下部署LAMP环境
tags:
  - Linux
  - LAMP
categories:
  - 技术
---

# Ubuntu20.04安装lamp基础环境

## 我的设备：

```bash
black@black-OMEN:~$ neofetch
            .-/+oossssoo+/-.               black@black-OMEN 
        `:+ssssssssssssssssss+:`           ---------------- 
      -+ssssssssssssssssssyyssss+-         OS: Ubuntu 20.04 LTS x86_64 
    .ossssssssssssssssssdMMMNysssso.       Host: OMEN by HP Laptop 
   /ssssssssssshdmmNNmmyNMMMMhssssss/      Kernel: 5.4.0-40-generic 
  +ssssssssshmydMMMMMMMNddddyssssssss+     Uptime: 1 hour, 58 mins 
 /sssssssshNMMMyhhyyyyhmNMMMNhssssssss/    Packages: 1637 (dpkg), 11 (snap) 
.ssssssssdMMMNhsssssssssshNMMMdssssssss.   Shell: bash 5.0.16 
+sssshhhyNMMNyssssssssssssyNMMMysssssss+   Resolution: 1920x1080 
ossyNMMMNyMMhsssssssssssssshmmmhssssssso   DE: GNOME 
ossyNMMMNyMMhsssssssssssssshmmmhssssssso   WM: Mutter 
+sssshhhyNMMNyssssssssssssyNMMMysssssss+   WM Theme: Adwaita 
.ssssssssdMMMNhsssssssssshNMMMdssssssss.   Theme: Yaru-dark [GTK2/3] 
 /sssssssshNMMMyhhyyyyhdNMMMNhssssssss/    Icons: Yaru [GTK2/3] 
  +sssssssssdmydMMMMMMMMddddyssssssss+     Terminal: gnome-terminal 
   /ssssssssssshdmNNNNmyNMMMMhssssss/      CPU: Intel i5-7300HQ (4) @ 3.500GHz 
    .ossssssssssssssssssdMMMNysssso.       GPU: Intel HD Graphics 630 
      -+sssssssssssssssssyyyssss+-         GPU: NVIDIA GeForce GTX 1050 Mobile 
        `:+ssssssssssssssssss+:`           Memory: 2511MiB / 11867MiB 
            .-/+oossssoo+/-.
                                                                   
                                                                
```

## 安装php, php-fpm, apache2(Nginx), mariadb-server

```bash
black@black-OMEN:~$ sudo apt install php php-fpm apache2 mariadb-server
```

### 配置mariadb-server

* 注意 **root** 运行

  ```bash
  black@black-OMEN:~$ sudo mysql_secure_installation
  # 首先会让你输入密码，因为是初次安装，所以直接回车即可
  # 然后会让你设置root密码，并确认
  # 之后的，一路回车即可
  ```

  此处不 **root** 运行`mysql_secure_installation`是会说你密码错误的。

* 运行服务

  ```bash
  black@black-OMEN:~$ sudo service mariadb restart
  ```

  进入试试：

  ```bash
  black@black-OMEN:~$ sudo mysql -u root -p
  Enter password: 
  Welcome to the MariaDB monitor.  Commands end with ; or \g.
  Your MariaDB connection id is 60
  Server version: 10.3.22-MariaDB-1ubuntu1 Ubuntu 20.04
  
  Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
  
  Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
  
  MariaDB [(none)]> show databases;
  +--------------------+
  | Database           |
  +--------------------+
  | information_schema |
  | mysql              |
  | performance_schema |
  +--------------------+
  3 rows in set (0.001 sec)
  ```

  至此成功。

### 配置apache2和php-fpm

* 首先停止这两个的服务

  ```bash
  black@black-OMEN:~$ sudo service apache2 stop
  black@black-OMEN:~$ sudo service php7.4-fpm stop
  ```

* 编辑apache2配置文件

  首先看下目录结构：

  ```bash
  black@black-OMEN:~$ cd /etc/apache2/
  black@black-OMEN:/etc/apache2$ ls
  apache2.conf  conf-available  conf-enabled  envvars  magic  mods-available  mods-enabled  ports.conf  sites-available  sites-enabled
  black@black-OMEN:/etc/apache2$ tree conf-available/
  conf-available/
  ├── charset.conf
  ├── localized-error-pages.conf
  ├── other-vhosts-access-log.conf
  ├── php7.4-fpm.conf
  ├── security.conf
  └── serve-cgi-bin.conf
  
  0 directories, 6 files
  ```

  由上面可以看到，在`conf-available`中已经有配置好的文件。那怎么让它生效呢？看下`conf-enabled`目录结构：

  ```bash
  black@black-OMEN:/etc/apache2$ tree conf-enabled/
  conf-enabled/
  ├── charset.conf -> ../conf-available/charset.conf
  ├── localized-error-pages.conf -> ../conf-available/localized-error-pages.conf
  ├── other-vhosts-access-log.conf -> ../conf-available/other-vhosts-access-log.conf
  ├── security.conf -> ../conf-available/security.conf
  └── serve-cgi-bin.conf -> ../conf-available/serve-cgi-bin.conf
  
  0 directories, 5 files
  ```

  由此可发现，实际上`conf-enabled`就是`conf-available`里的软连接，因此，**我们只需要在`conf-enabled`里创建`conf-available/php7.4-fpm.conf`的软链接即可**。

  ```bash
  black@black-OMEN:/etc/apache2$ cd conf-enabled/
  black@black-OMEN:/etc/apache2/conf-enabled$ sudo ln -s ../conf-available/php7.4-fpm.conf 
  # 此时查看enabled情况，发现已经被添加到了。
  black@black-OMEN:/etc/apache2/conf-enabled$ tree .
  .
  ├── charset.conf -> ../conf-available/charset.conf
  ├── localized-error-pages.conf -> ../conf-available/localized-error-pages.conf
  ├── other-vhosts-access-log.conf -> ../conf-available/other-vhosts-access-log.conf
  ├── php7.4-fpm.conf -> ../conf-available/php7.4-fpm.conf
  ├── security.conf -> ../conf-available/security.conf
  └── serve-cgi-bin.conf -> ../conf-available/serve-cgi-bin.conf
  
  0 directories, 6 files
  ```

  **注意：**因为我这里装的正好就是`php7.4-fpm`，而且是通过`apt`装的，所以使用默认即可，如果你不是用的默认的，则还需要修改下`php7.4-fpm.conf`中的参数。

* 重启服务，测试

  ```bash
  # 启动服务
  black@black-OMEN:/etc/apache2/conf-enabled$ sudo service apache2 restart
  black@black-OMEN:/etc/apache2/conf-enabled$ sudo service php7.4-fpm restart
  ```

  测试`html`

  ```
  black@black-OMEN:/etc/apache2/conf-enabled$ sudo vim /var/www/html/test.html
  ```

  此时若访问[localhost/test.html](localhost/test.html)配置即完成。

  测试`.php`

  ```bash
  black@black-OMEN:/etc/apache2/conf-enabled$ sudo vim /var/www/html/test.php
  ```

  写入：

  ```php
  <?php
      phpinfo();
  ?>
  ```

  此时若访问[localhost/test.php](localhost/test.php)配置即完成。

