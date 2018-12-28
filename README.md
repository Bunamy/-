# -静态爬虫
例子
import sys
from bs4 import BeautifulSoup
import requests
class pa(object):
    def __init__(self,ip,ipplus,flag,flag1):
         self.ip=ip
         self.ipplus=ipplus
         self.flag=flag
    def get_contents(self):
         req=requests.get(url=self.ip)
         html=req.text
         ss=BeautifulSoup(html)
         contents=ss.find_all(self.flag)
         contents=contents[0].replace('\xa0'*8,'\n\n')
         return contents
    def get_chapter(self):
         req=requests.get(url=self.ip)
         html=req.text
         ss=BeautifulSoup(html)
         mulu=ss.find_all(
