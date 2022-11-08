---
title: mysql 8.0.31 安装配置全过程
categories: mysql
comments: true
highlight_shrink: false
abbrlink: fe9d3ff6
date: 2022-11-07 00:00:00
updated:
---

## mysql 8.0.31 安装配置全过程

### 1. 下载
[MySQL Community Downloads](https://dev.mysql.com/downloads/mysql/)
下载需要用 Oracle 账号登录，百度自行搜索。

最好下载压缩包，方便管理和配置。

### 2. 配置

#### 2.1 解压

#### 2.2 初始化
进入 bin 目录，在当前目录下 cmd，输入
```cmd
mysqld --initialize --console
```
记住当前的密码（MqGsepr&S0&e）！
![init](/images/mysql-安装配置/init.png)


#### 2.3 安装 mysql 服务
用管理员身份启动 cmd，进入 bin 目录，输入
```cmd
mysqld -install
```
![installServer](/images/mysql-安装配置/installServer.png)
可以看到已经有了 mysql 服务了。
![mysqlServer](/images/mysql-安装配置/mysqlServer.png)

#### 2.4 启动和关闭服务
启动和关闭服务一种是在 Windows 服务中手动开启和关闭，另一种是用命令来启动和关闭。
```cmd
net stop mysql
net start mysql
```
![startService](/images/mysql-安装配置/startService.png)

#### 3.5 修改密码
输入
```cmd
mysql -u root -p
// 之前初始化的密码
alter user 'root'@'localhost' identified by '密码';
commit;
```
![alterPassword](/images/mysql-安装配置/alterPassword.png)