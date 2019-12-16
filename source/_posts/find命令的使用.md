---
title: find命令的使用
tags: Ubuntu
categories: Ubuntu
comments: true
date: 2019-04-03 20:55:05
---


例子：find / -name "*.txt" -exec ls -l {} \;

解释：这条命令的作用是 从根目录开始按文件名查找出所有的txt文件并以长格式列出的方式显示出来



find [目录] [选项] [选项参数] [后续动作]
<!--more-->

/ 表示根目录

类似的还有：

./ 当前目录

../ 上级目录

～ 家目录



常用选项：

atime：访问时间（access time），指的是文件最后被读取的时间

ctime：变更时间（change time），指的是文件本身（权限、所属组、位置......）最后被变更的时间

mtime：修改时间（modify time），指的是文件内容最后被修改的时间

-name 文件名：根据文件名查找文件

-size [+-]SIZE：查找比SIZE还要大（+）或小（-）的文件

-type TYPE：查找文件类型为TYPE的

-perm mode：查找文件权限“刚好等于”mode的文件



-exec 命令：-exec后面可再接其他的命令来处理查到的结果



ls -l 长格式列出，相当于ll

 

{}：代表的是“由find找到的内容”



\ 用来转义;



; 表示额外的命令结束