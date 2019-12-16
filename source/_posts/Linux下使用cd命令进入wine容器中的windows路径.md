---
title: Linux下使用cd命令进入wine容器中的windows路径
tags: Ubuntu
categories: Ubuntu
comments: true
date: 2019-04-03 21:16:10
---


今天在使用Ubuntu系统时，想卸载wine中安装的TIM版QQ

需要进入安装目录下使用 wine TIMUninst.exe命令

结果死活cd不进去
<!--more-->
原目录: ~/.wine/drive_c/Program Files (x86)/Tencent/TIM/TIMUninst.exe

中间Program Files (x86)用tab补齐和"\"拼接都过不去

解决办法:使用双引号将这段含有空格的目录引起来

完整目录:.wine/drive_c/"Program Files (x86)"/Tencent/TIM/TIMUninst.exe

cd +完整目录就可以进去了