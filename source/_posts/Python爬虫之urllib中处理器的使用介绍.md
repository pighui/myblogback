---
title: Python爬虫之urllib中处理器的使用介绍
comments: true
tags:
  - Python
  - 爬虫
categories: 爬虫
date: 2019-04-20 21:09:58
---


本文将介绍urllib库中的各种处理器以及使用方法。

1.HTTPHandler 请求处理器

2.ProxyHandler 代理处理器

3.HTTPCookieProcessor Cookie处理器

4.使用opener对象请求，类似于浏览器

<!--more-->

# 1.HTTPHandler 请求处理器

使用urllib库中的Handler处理器
1）处理器需要添加到opener 浏览器对象中
2）所有的请求(Request)将会由opener打开

```python
#! /usr/bin/env python
# -*-coding:UTF-8-*-
#__author__ : pighui
#__time__ : 2019-4-18 下午4:12


from urllib.request import Request, build_opener, HTTPHandler
from util.header import get_header
from util.html import get_charset,to_html

def request(url):
    #1.创建一个opener对象 -- 类似于一个浏览器
    opener = build_opener(HTTPHandler())

    #2.构建请求对象 Request
    req = Request(url, headers=get_header())

    #3.发起请求
    resp = opener.open(req)
    #print(type(resp)) #http.client.HTTPResponse
    if resp.code == 200:
        content_type = resp.getheader('Content-Type')
        charset = get_charset(content_type)
        html = to_html(resp.read())
    print(html)

if __name__ == '__main__':
    url = 'https://www.xuhuiblog.cn'
    request(url)
```

# 2.ProxyHandler 代理处理器

处理IP代理处理器 urllib.request.ProxyHandler
1) 处理器一定与opener一块使用, urllib.request.build_opener()
2) ProxyHandler也可以和HTTPHandler、HTTPCookieProcessor一起组合使用
3）ProxyHandler创建时，需要提供一个proxies 参数

proxies给定是一个字典对象， 如
{'http': '10.11.11.90:8776',

'https': '98.12.11.12:80' }

```python
import re
from urllib.request import build_opener, HTTPHandler, ProxyHandler, Request

from util import header
import ssl
ssl._create_default_https_context = ssl._create_unverified_context


def get(url, proxies):
    opener = build_opener(HTTPHandler(),
                          ProxyHandler(proxies))
    resp = opener.open(Request(url, headers=header.get_headers()))
    if resp.code == 200:
        print('--请求成功--')
        html = resp.read()
        html_text = html.decode()
        s = re.findall(r"<a href='/ipv4/\d+\.\d+\.\d+\.\d+'>(\d+\.\d+\.\d+\.\d+)</a>", html_text)

        print('当前主机的IP: ', s)


if __name__ == '__main__':
    # 从免费的IP代理网站获取代理的ip、port、类型(http/https)
    proxies = {
        # 'HTTPS': '119.102.24.141:9999'
        'http': '119.102.29.228:9999'
    }
    get('https://zh-hans.ipshu.com/my_info', proxies)
```



# 3.HTTPCookieProcessor Cookie处理器

CookieJar和HTTPCookieProcess处理器的应用
1）login接口，实现登录操作
2）登录之后，在请求个人中心，获取个人收藏的信息

使用的步骤
1）创建http.cookiejar.CookieJar  类对象
2）创建urllib.request.HTTPCookieProcess对象，并传入CookieJar对象
3）将HTTPCookieProcess对象添加到opener

```python
from http.cookiejar import CookieJar
from urllib.parse import urlencode
from urllib.request import HTTPHandler, HTTPCookieProcessor, build_opener, Request

from util import html, header

from lxml import etree

# 让opener具有HTTP请求的能力
# 和Cookie信息的处理能力
opener = build_opener(
    HTTPHandler(),
    HTTPCookieProcessor(CookieJar())
)


def request(url, data: dict, headers: dict):
    # 将post上传的数据转成字节流
    form_params = urlencode(data)  # key=value&key2=value2
    req = Request(url, form_params.encode(), headers)

    # 登录
    resp = opener.open(req)

def get(url, headers):

    resp = opener.open(Request(url, headers=headers))
    html_text = html.to_html(resp.read(),
                             html.get_charset(resp.getheader('Content-Type')))

    root = etree.HTML(html_text)
    account = root.xpath('//p[@class="pt5"]/span/text()')[0]
    print(account)

if __name__ == '__main__':
    login_url = 'http://www.renren.com/ajaxLogin/login?1=1&uniqueTimestamp=20182122180'
    info_url = 'http://www.renren.com/224549540/profile'

    data = {
        'rkey': '1c7df63368df7ce73c234de26178ec11',
        'password': '19870115',
        'origURL': 'http://www.renren.com/home',
        'key_id': '1',
        'icode': '',
        'f': 'http://www.renren.com/224549540',
        'email': 'dqsygcz@126.com',
        'domain': 'renren.com',
        'captcha_type': 'web_login',
    }

    # request(login_url, data, headers=header.get_headers())
    # headers请求中已经包含了当前url站点的登录后的Cookie信息
    # 可以收集多个账号登录之后的Cookie信息，作为Cookie池
    get('http://user.sc.chinaz.com/index.aspx', headers=header.get_headers())
```

