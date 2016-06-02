---
title: scrapy 初探
date: 2016-06-02 16:39:57
tags: [Python,scrapy]
---
Python下的爬虫框架初探
```Python
import requests
from bs4 import BeautifulSoup

headers = {
    'User-Agent': 'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:22.0) Gecko/20100101 Firefox/22.0'
}

def save_jpg(res_url):
    html = BeautifulSoup(requests.get(res_url,headers=headers).text)
    for index,each in enumerate(html.select('.artist-container img')):
        with open('{}.jpg'.format(each.attrs['alt']), 'wb') as jpg:
            print('http://www.141jav.com'+ each.attrs['src'])
            jpg.write(requests.get('http://www.141jav.com'+each.attrs['src'], stream=True).content)

if __name__ == '__main__':
    starturl = 'http://www.141jav.com/'
    html = BeautifulSoup(requests.get(starturl,headers=headers).text)
    for index,each in enumerate(html.select('.resources a',limit=14)):
        print(index,'http://www.141jav.com'+each.attrs['href'])
        save_jpg('http://www.141jav.com'+each.attrs['href'])
```