---
layout: post
title: ��Pythonʵ��Webscraping
tag: Python 
---

###How to get data? 
**1.ͨ���ض��İ���ȡ�ض����ݣ�������һ��д�õ�Webscraping����**

Demo: tushare��tushare��Python��һ���ƾ����ݽӿڰ���

> import tushare as ts  
> df = ts.get_hist_data('000002') #��ȡ������ȫ����k������
> df.head(10) # pandas��DataFrame���ݽṹ����ӡǰ10����¼

����tushare���÷�����[baidu](https://jingyan.baidu.com/article/3065b3b68d7fb5becff8a494.html)

**2. Webscraping by yourself**

###How to scrape web data?

>*  crawl webpages: urllib, requests, etc.
>*  parse webpages: BeautifulSoup, re (regular expression), etc.
>*  more sophisicated framework for large-scale crawling: Scrapy, search engines

 
**Requestsץȡ��ҳ��ͨ�ô���: �����쳣���񣬳�ʱ�趨�������趨�������αװ**
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
**BeautifulSoup��������������������ά������ǩ�����Ĺ��ܿ�**

BeautifulSoup��Ļ���Ԫ��
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


