---
title: 对于Python中多线程的理解及实现方法
comments: true
tags:
  - Python
  - 爬虫
categories: 爬虫
date: 2019-04-16 20:17:26
---




本文使用四个例子，向大家介绍如何使用threading库。

安装包

```bash
pip install threading
```

<!--more-->

#### 1.线程的简单使用

用法基本和进程相同，使用threading库
步骤：
——使用threading.Thread类,创建爱你线程对象
——使用线程对象启动线程 - start
——使用线程对象调用.join()等待线程完成



```python
#! /usr/bin/env python
# -*-coding:UTF-8-*-
#__author__ : pighui
#__time__ : 2019-4-16 上午11:13


import csv
import threading
import time

#注：多线程是共享同一进程的内存空间
is_stop = False # 停止读取线程的标识，可以用在多个子线程

def read_csv(filepath):
    """
    读取csv文件中的数据，每隔一秒钟显示一行
    """
    with open(filepath) as f:
        reader = csv.DictReader(f,
                                fieldnames=('REPOSITORY','TAG','IMAGE','ID','CREATED','SIZE'))
        for row in reader:
            #通过标识位的方式中断线程
            if is_stop: break
            #获取当前线程的名称
            thread_name = threading.currentThread().name
            print(thread_name,row)
            time.sleep(1)

def delay_stop(delay):
    #延迟delay时间后尝试关闭子线程
    print(threading.current_thread().name, '延迟 %ss中断读取线程\n' % delay)
    time.sleep(delay)
    global is_stop
    is_stop = True



if __name__ == '__main__':
    #1. 创建线程对象
    # Thread()中参数同Process()中参数
    thread = threading.Thread(target=read_csv,
                              args=('images.csv',))
    #2. 启动线程
    thread.start()  #异步执行
    print(threading.current_thread().name, '--正在读取--')
    #启动
    threading.Thread(target=delay_stop,args=(5,)).start()
    #3. 等待子线程执行完成
    thread.join()   #同步执行，阻塞到线程执行完
    #如果线程正在运行，如何中断
    '''
    thread.is_alive()  #判断线程是否存活
    #可以使用标识符
    '''
    print('--over--')
```

#### 2.多线程是共享内存的

如果多个线程同时操作一个变量或对象时，可能会造成数据冗余或数据丢失。

使用threading下的Lock函数创建线程锁

```python
#! /usr/bin/env python
# -*-coding:UTF-8-*-
#__author__ : pighui
#__time__ : 2019-4-16 上午11:49


from threading import Thread, current_thread, Lock
import time

money = 1000
lock = Lock()


def add(m):
    global money
    #存入m的钱数

    #进入上下文时，调用Lock对象的__enter__函数-->lock.acquire()
    #退出上下文时，调用Lock对象的__exit__函数-->lock.release()
    with lock:
        print(current_thread().name,
              '当前余额：', money,
              '本次存入：', m)
        money += m
        time.sleep(1)
        print(current_thread().name,
              '存放后的余额:', money)

def sub(m):
    global money
    #取m的钱数
    with lock:
        print(current_thread().name,
              '当前余额：', money,
              '本次取出：', m)
        money -= m
        time.sleep(1)
        print(current_thread().name,
              '取出后的余额:', money)


if __name__ == '__main__':
    #模拟同一账户下，3人存钱，2人取钱
    add_threads = [
        Thread(target=add, args=(m, ))
        for m in (1000, 2000, 3000)
    ]

    sub_threads = [
        Thread(target=sub, args=(m, ))
        for m in (500, 2500)
    ]

    for thread in add_threads+sub_threads:
        thread.start()

    for thread in add_threads+sub_threads:
        thread.join()

    print('最终的余额:', money)
```

#### 3.线程的本地变量

问题描述：
1）多线程中访问的公共的变量都是共享同一内存的
2）如果使用同一名字，且作用范围只限于本线程的话，只能使用本地变量

local() 线程本地变量
1）每隔线程中的变量，类似于dict的结构，key是当前线程对象
2）v.money = 0 向v中添加一个线程本地变量

```python
#! /usr/bin/env python
# -*-coding:UTF-8-*-
#__author__ : pighui
#__time__ : 2019-4-16 下午4:21


import random
import time
from threading import current_thread, local, Thread

v = local() #创建线程本地变量
v.money = 1000

def new_add(m):
    global v
    print(current_thread().name,'-->准备开户')
    v.money = 0 #向本地变量添加属性
    '''开户并存钱'''
    print(current_thread().name,
          '存入%s元'%m, '余额%s元\n'%v.money)
    v.money += m
    print(current_thread().name,
          '余额%s元'%v.money)
    time.sleep(1)
if __name__ == '__main__':
    #模拟十人开户并存钱
    add_threads = [
        Thread(target = new_add, args=(random.randint(100,1000),))
        for _ in range(10)
    ]
    for thread in add_threads:
        thread.start()
    for thread in add_threads:
        thread.join()
```

#### 4.设计模式中的生产者与消费者
1）线程的条件变量和线程锁
2）queue.Queue 队列——存储数据
3）自定义同步的Queue

```python
#! /usr/bin/env python
# -*-coding:UTF-8-*-
#__author__ : pighui
#__time__ : 2019-4-16 下午4:21


'''
线程的本地变量
问题描述：
1）多线程中访问的公共的变量都是共享同一内存的
2）如果使用同一名字，且作用范围只限于本线程的话，只能使用本地变量

local() 线程本地变量
1）每隔线程中的变量，类似于dict的结构，key是当前线程对象
2）v.money = 0 向v中添加一个线程本地变量
'''


import random
import time
from threading import current_thread, local, Thread

v = local() #创建线程本地变量
v.money = 1000

def new_add(m):
    global v
    print(current_thread().name,'-->准备开户')
    v.money = 0 #向本地变量添加属性
    '''开户并存钱'''
    print(current_thread().name,
          '存入%s元'%m, '余额%s元\n'%v.money)
    v.money += m
    print(current_thread().name,
          '余额%s元'%v.money)
    time.sleep(1)
if __name__ == '__main__':
    #模拟十人开户并存钱
    add_threads = [
        Thread(target = new_add, args=(random.randint(100,1000),))
        for _ in range(10)
    ]
    for thread in add_threads:
        thread.start()
    for thread in add_threads:
        thread.join()
```

