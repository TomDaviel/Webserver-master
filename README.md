# WebServer
用C++实现的高性能WEB服务器，经过webbenchh压力测试可以实现上万的QPS

## 功能
* 利用IO复用技术Epoll与线程池实现多线程的Reactor高并发模型；
* 利用正则与状态机解析HTTP请求报文，实现处理静态资源的请求；
* 利用标准库容器封装char，实现自动增长的缓冲区；
* 基于小根堆实现的定时器，关闭超时的非活动连接；
* 利用单例模式与阻塞队列实现异步的日志系统，记录服务器运行状态；
* 利用RAII机制实现了数据库连接池，减少数据库连接建立与关闭的开销，同时实现了用户注册登录功能。

* 增加logsys,threadpool测试单元(todo: timer, sqlconnpool, httprequest, httpresponse) 

## 环境要求
* Linux
* C++14
* MySql

## 快速开始

- 安装MySQL以及相关库

  ```bash
  sudo apt install mysql-server//服务
  sudo apt-get install libmysqlclient-dev//C++-Mysql链接库
  ```

- 测试前建库
  ```
  sudo service mysql start
  mysql -u root -p
  ```

  ```mysql
  // 建立yourdb库
  create database yourdb;
  
  // 创建user表
  USE yourdb;
  CREATE TABLE user(
      username char(50) NULL,
      passwd char(50) NULL
  )ENGINE=InnoDB;
  
  // 添加数据用于Web登陆
  INSERT INTO user(username, passwd) VALUES('name', 'passwd');

  exit
  ```
  

- 修改main.cpp中的数据库初始化信息

  ```mysql
  //数据库登录名,密码,库名
  string user = "root";
  string passwd = "";
  string databasename = "yourdb";
  ```

- build

  ```
  sh ./build.sh
  ```

- 启动server

  ```
  ./server
  ```

- Windows浏览器访问端口

  ```
  localhost:9006
  ```

## 压力测试
* 测试环境: WSL2 Ubuntu:22.04
* QPS 10000+