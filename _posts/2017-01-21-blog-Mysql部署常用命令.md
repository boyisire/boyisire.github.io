---
layout:     post
title:      "Mysql部署常用命令"
subtitle:   "Mysql部署常用命令"
date:       2017-01-21 11:35:00
author:     "大业"
header-img: ""
catalog: true
tags:
    - 数据库
    - Mysql
---

* content
{:toc}

安装mysql后,需要对数据库进行基本的配置操作,下面是平时常用的一些命令





##Mysql配置
### 1. 设置外网用户可访问
打开：  
`/etc/mysql/my.cnf`
修改该项为:  
`bind-address            = 0.0.0.0`

用root登录mysql,修改host为任意主机,并刷新权限到内存中。
执行命令集:
```
mysql> update `user` set `host` = '%' where `user` = 'root';  
mysql> flush privileges; 
```

##Mysql操作
### 1. 登录mysql
`mysql -u root -p`

### 2. 新建用户
> 注意：此处的Host列，是指该用户在本地登录还是在远程登录.
如果本地，写:"localhost";
如果远程，写:"%",想远程登录的话.

`INSERT INTO mysql.user(Host,User,Password) values("%","webdba",password("******************"));`
或者
`CREATE USER 'webdba'@'%' IDENTIFIED BY '******************'; `

### 3. 给用户授权
> 格式：grant 权限 on 数据库.* to 用户名@登录主机 identified by "密码";

所有权限
`grant all privileges on bbs.* to webdba@"%" identified by "******************";`
部分权限
`grant select,delete,update,insert,create on bbs.* to test@"%" identified by "***********************";`
> 格式：grant 权限 on 数据库.* to 用户名@登录主机 identified by "密码";

### 4. 回收root管理员密码
`SET PASSWORD FOR 'root'@'%' = PASSWORD('XXXXX');`
或
`update mysql.user set password=password('新密码') where User="root" and Host="%";`
