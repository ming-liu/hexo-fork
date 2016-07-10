---
title: centos_wordpress
date: 2016-02-18 13:10:40
tags:
---


### Aliyun Ecs Centos 64bit .install wordpress

#### 1、install apache

1.1 查询是否安装，若没有返回信息则没有安装。
	```	bash
	rpm -qa httpd 
	```
1.2 安装apache。
	```	bash
	yum install httpd -y
	```
1.3 启动
	```	bash
	service httpd start
	service httpd stop
	service httpd restart
	```

#### 2、install mysql

2.1 查询mysql是否安装
	``` bash
	rpm -qa mysql
	```
2.2 查询yum服务器上mysql
	``` bash
	yum list | grep mysql
	```
2.3 安装mysql
	```
	yum install -y mysql-server mysql-devel mysql
	```
2.4 mysql是否自动启动,设置mysqld自动启动
	```
	chkconfig --list | grep mysql
	chkconfig mysqld on
	```

2.5 启动mysql
	```
	service mysqld start
	```
2.6 修改密码
	```
	mysqladmin -u root password ''

	```

#### 3、install php

3.1 安装php
	``` bash
	yum install php php-devel
	```
3.2 安装php扩展
	``` bash
	yum install php-gd php-imap php-ldap php-odbc php-pear php-xml php-xmlrpc
	```
#### 4、install ftp

4.1 install ftp
	``` bash
	yum -y install vsftpd 
	```
4.2 取消匿名登录
	```
	vi /etc/vsftpd/vsftpd.conf
	anonymous_enable=NO
	```
4.3 创建一个用户
	```
	useradd ftpuser 
	passwd ftpuser 
	```
	



	