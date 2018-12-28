# -静态爬虫
例子
import sys
from bs4 import BeautifulSoup
import requests
class pa(object):
    def __init__(self,ip,ipplus,flag,flag1,cara,deleterow,path):
         self.ip=ip
         self.ipplus=ipplus
         self.flag=flag
         self.cara=cara
         self.deleterow=deletrow
         self.path=path
    def get_contents(self,ip):
         req=requests.get(url=ip)
         html=req.text
         ss=BeautifulSoup(html)
         contents=ss.find_all(self.flag)
         contents=contents[0].replace('\xa0'*8,'\n\n')
         return contents
    def get_chapter(self):
         req=requests.get(url=self.ip)
         html=req.text
         ss=BeautifulSoup(html)
         mulu=ss.find_all(self.flag1)
         mulu=BeatifulSoup(str(mulu[0])
         mulu=mulu.find_all(self.cara)
         chaptername=[]
         urls=[]
         for each in a[self.deleterow:]:
            chaptername.append(each.string)
            urls.append(self.ipplus + each.get('href'))
         return chaptername,urls
    def writer(self,chaptername,contents):
         with open(self.path,'a',encoding='utf-8') as f
         f.write(chaptername +'\n')
         f.writelines(contents)
         f.write('\n\n')
    def run(self):
         chaptername,urls=self.get_chapter()
         print "开始下载"
         for i in range(len(urls)):
            contents=self.get_contents(urls[i])
            chaptername=chaptername[i]
            self.writer(chaptername,contents)
         print "下载完成"
         
         
