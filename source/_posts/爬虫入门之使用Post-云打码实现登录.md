---
title: 爬虫入门之使用Post+云打码实现登录
comments: true
tags:
  - Python
  - 爬虫
categories: 爬虫
date: 2019-04-19 20:18:35
---



本文将介绍的是如何使用urllib中的处理器+云打码api调用实现验证码登录。

准备工作：

​	在[云打码](<http://www.yundama.com/>)平台注册，并购买一定数量的验证码条数。

<!--more-->

#### 1.登录脚本

目标连接：<https://www.gushiwen.org/>

CookieJar和HTTPCookieProcess处理器的应用
1） login接口，实现登录操作
2） 登录之后，再请求个人中心，获取个人收藏的信息

使用的步骤
1) 创建http.cookiejar.CookieJar 类对象
2) 创建urllib.request.HTTPCookieProcessor对象，并传入CookieJar对象
3）将HTTPCookieProcess对象添加到opener

```python

from http.cookiejar import CookieJar
from urllib.parse import urlencode
from urllib.request import HTTPHandler, HTTPCookieProcessor, build_opener, Request
from urllib.request import urlretrieve

from util import html, header, ydm_api

from lxml import etree
import ssl
ssl._create_default_https_context = ssl._create_unverified_context

# 让opener具有HTTP请求的能力
# 和Cookie信息的处理能力
opener = build_opener(
    HTTPHandler(),
    HTTPCookieProcessor(CookieJar())
)


def request(url, data: dict, headers=None):
    if data:
        # 将post上传的数据转成字节流
        form_params = urlencode(data)  # key=value&key2=value2
        req = Request(url, form_params.encode(), headers)
    else:
        if headers:
            req = Request(url, headers=headers)
        else:
            req = Request(url)

    resp = opener.open(req)
    html_txt = html.to_html(resp.read(),
                            html.get_charset(resp.getheader('Content-Type')))
    print(html_txt)



if __name__ == '__main__':
    login_url = 'https://so.gushiwen.org/user/login.aspx?from=http%3a%2f%2fso.gushiwen.org%2fuser%2fcollect.aspx'
    collect_url = 'https://so.gushiwen.org/user/collect.aspx'

    # 验证码的图片
    code_url = 'https://so.gushiwen.org/RandCode.ashx'


    #urlretrieve(code_url, 'code.png') # 刷新并保存验证图片
    resp = opener.open(code_url)
    with open('code.png', 'wb') as file:
        file.write(resp.read())



    # 注意： ydm_api模块，需要安装requests库
    # pip install requests
    result = ydm_api.ydm('code.png')
    print('验证码的结果：', result)
    data = {
        'action':'',
        'from':'http://so.gushiwen.org/user/collect.aspx',
        'email': '账号',
        'pwd': '密码',
        'code': result  # 验证码， 第三方平台的API解码
    }

    request(login_url, data, headers=header.get_headers())
    # request(collect_url)



```

#### 2.云打码平台接口调用脚本

```python
import http.client, mimetypes, urllib, json, time, requests


######################################################################

class YDMHttp:
    apiurl = 'http://api.yundama.com/api.php'
    username = ''
    password = ''
    appid = ''
    appkey = ''

    def __init__(self, username, password, appid, appkey):
        self.username = username
        self.password = password
        self.appid = str(appid)
        self.appkey = appkey

    def request(self, fields, files=[]):
        response = self.post_url(self.apiurl, fields, files)
        response = json.loads(response)
        return response

    def balance(self):
        data = {'method': 'balance', 'username': self.username, 'password': self.password, 'appid': self.appid,
                'appkey': self.appkey}
        response = self.request(data)
        if (response):
            if (response['ret'] and response['ret'] < 0):
                return response['ret']
            else:
                return response['balance']
        else:
            return -9001

    def login(self):
        data = {'method': 'login', 'username': self.username, 'password': self.password, 'appid': self.appid,
                'appkey': self.appkey}
        response = self.request(data)
        if (response):
            if (response['ret'] and response['ret'] < 0):
                return response['ret']
            else:
                return response['uid']
        else:
            return -9001

    def upload(self, filename, codetype, timeout):
        data = {'method': 'upload', 'username': self.username, 'password': self.password, 'appid': self.appid,
                'appkey': self.appkey, 'codetype': str(codetype), 'timeout': str(timeout)}
        file = {'file': filename}
        response = self.request(data, file)
        if (response):
            if (response['ret'] and response['ret'] < 0):
                return response['ret']
            else:
                return response['cid']
        else:
            return -9001

    def result(self, cid):
        data = {'method': 'result', 'username': self.username, 'password': self.password, 'appid': self.appid,
                'appkey': self.appkey, 'cid': str(cid)}
        response = self.request(data)
        return response and response['text'] or ''

    def decode(self, filename, codetype, timeout):
        cid = self.upload(filename, codetype, timeout)
        if (cid > 0):
            for i in range(0, timeout):
                result = self.result(cid)
                if (result != ''):
                    return cid, result
                else:
                    time.sleep(1)
            return -3003, ''
        else:
            return cid, ''

    def report(self, cid):
        data = {'method': 'report', 'username': self.username, 'password': self.password, 'appid': self.appid,
                'appkey': self.appkey, 'cid': str(cid), 'flag': '0'}
        response = self.request(data)
        if (response):
            return response['ret']
        else:
            return -9001

    def post_url(self, url, fields, files=[]):
        for key in files:
            files[key] = open(files[key], 'rb');
        res = requests.post(url, files=files, data=fields)
        return res.text


######################################################################

# 用户名（普通用户名）
username = '你的用户名'

# 密码
password = '你的密码'

# 软件ＩＤ，开发者分成必要参数。登录开发者后台【我的软件】获得！
appid = 5100

# 软件密钥，开发者分成必要参数。登录开发者后台【我的软件】获得！
appkey = '2a05b965cea2553a378bc2955c4756a5'

# 验证码类型，# 例：1004表示4位字母数字，不同类型收费不同。请准确填写，否则影响识别率。在此查询所有类型 http://www.yundama.com/price.html
codetype = 1004

# 超时时间，秒
timeout = 60


def ydm(filename):
    # 初始化
    yundama = YDMHttp(username, password, appid, appkey)

    # 登陆云打码
    uid = yundama.login();
    print('uid: %s' % uid)

    # 查询余额
    balance = yundama.balance();
    print('balance: %s' % balance)

    # 开始识别，图片路径，验证码类型ID，超时时间（秒），识别结果
    cid, result = yundama.decode(filename, codetype, timeout);
    print('cid: %s, result: %s' % (cid, result))
    return result
    ######################################################################

```

