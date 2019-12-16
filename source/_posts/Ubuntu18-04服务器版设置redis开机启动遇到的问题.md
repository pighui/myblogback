---
title: Ubuntu18.04服务器版设置redis开机启动遇到的问题
tags: Ubuntu
categories: Ubuntu
comments: true
date: 2019-04-03 21:04:43
---


![](Ubuntu18-04服务器版设置redis开机启动遇到的问题/redis.png)

最后一句话意为

启用单元失败：拒绝操作链接单元文件redis.service
<!--more-->
修改命令为

sudo systemctl enable redis-server.service

回车输入五次root密码就好了