---
title: Python中yield关键字的用法及运行逻辑
tags: Python
categories: Python
comments: true
date: 2019-04-03 21:11:35
---


以下面这段代码为例：

```python
def fun():
    print("进入fun函数了")
    x = yield 100
    print("在fun函数中的x：",x)
    yield "谢谢，你也快乐"
```

<!--more-->

```python
f = fun()
result = next(f)
print(result)
result2 = f.send("元宵节快乐")
print("程序外面的result2：",result2)
```

运行结果：

```
进入fun函数了
100
在fun函数中的x ：元宵节快乐
程序外面的result2 ：谢谢，你也快乐
```

逻辑思考：

```
f = fun()                             调用fun函数，控制台输出 “进入fun函数了”，执行到yield时等待next调用
result = next(f)                      yield继续执行，将100返回给result，函数挂起，此时x并没有被赋值
print(result)                         控制台打印100
result2 = f.send("元宵节快乐")        end方法将“元宵节快乐”发送至函数挂起之后的时刻，此时x被赋值为“元宵节快																		乐”，函数继续运行，在控制台打印“在fun函数中的x ：元宵节快乐” ，函数继续运																		行，再次遇到yeild关键字，并将“谢谢，你也快乐”返回到send之后的时刻，此时																			result2被赋值为“谢谢，你也快乐”，函数执行完毕
print("程序外面的result2：",result2)  控制台打印“程序外面的result2 ：谢谢，你也快乐”　　
```

