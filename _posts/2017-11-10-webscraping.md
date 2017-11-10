---
layout: post
title: 用Python实现Webscraping
tag: Python
---

###How to get data?
**1.ͨ通过特定的包获取数据（本质是一个写好的Webscraping包**

Demo: tushare（tushare是Python的一个财经数据接口包）

> import tushare as ts  
> df = ts.get_hist_data('000002') # 获取三年内全部日K线数据

更多tushare的用法可以去[baidu](https://jingyan.baidu.com/article/3065b3b68d7fb5becff8a494.html)

**2. Webscraping by yourself**

###How to scrape web data?

>*  crawl webpages: urllib, requests, etc.
>*  parse webpages: BeautifulSoup, re (regular expression), etc.
>*  more sophisicated framework for large-scale crawling: Scrapy, search engines


**Requests抓取网页的通用代码：加入异常捕获，超时设定，编码设定，浏览器伪装**
> import requests
> def get_html(url):# define get_html() function
>    try:
>         r = requests.get(url, headers={'User-Agent':'Mozilla/5.0'}, timeout=30)
>         r.raise_for_status() # throw HTTPError if the status code is not 200
>         r.encoding = r.apparent_encoding # handling encoding issue
>         return r.text
>     except:
>         return "Error: something is Wrong!"

###Parse webpages by BeautifulSoup
**BeautifulSoup库是用来解析、遍历、维护“标签树”的功能库**

BeautifulSoup类的基本元素
>* <p class="title">...</p>

How to use?

> from bs4 import BeautifulSoup
> import requests
> url = "http://www.crummy.com/software/BeautifulSoup"
> r = requests.get(url)
> soup = BeautifulSoup(r.text,"lxml")## get BeautifulSoup object
> link_list = [link.get('href') for link in soup.find_all('a')] ## get all links in the page
> ##if it starts with 'http' we are happy
> [link for link in link_list if link is not None and link.startswith('http')]
