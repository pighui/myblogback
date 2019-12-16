---
title: Ubuntu18.04完全卸载mysql
tags: Ubuntu
categories: Ubuntu
comments: true
date: 2019-04-03 21:20:05
---

#### 1.卸载mysql

```bash
sudo apt-get autoremove --purge mysql-server
sudo apt-get autoremove --purge mysql-server-*
sudo apt-get autoremove --purge mysql-client
sudo apt-get autoremove --purge mysql-client-*
sudo apt-get remove mysql-common
```
#### <!--more-->

#### 2.删除数据

```bash
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P 
```

注意，清楚的过程中会弹出几个窗口，内容大概是问你是否需要清除用户数据之类的，要选择yes！

#### 3.删除目录

```bash
sudo rm -rf /etc/mysql
sudo rm -rf /var/lib/mysql
```

#### 4.清除残留

```bash
sudo apt autoremove
sudo apt autoclean
```

到此完成。

