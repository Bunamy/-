from bs4 import BeautifulSoup
import requests
class pa(object):
    def __init__(self,ip,ipplus,flag,flag_class,flag1,flag1_class,cara,deleterow,path):
         self.ip=ip
         self.ipplus=ipplus
         self.flag=flag
         self.flag_class=flag_class
         self.flag1=flag1
         self.flag1_class=flag1_class
         self.cara=cara
         self.deleterow=deleterow
         self.path=path
    def get_contents(self,ip):
         req=requests.get(url=ip)
         html=req.text
         ss=BeautifulSoup(html,'lxml')
         contents=ss.find_all(self.flag,class_=self.flag_class)
         contents=contents[0].text.replace('\xa0'*8,'\n\n')
         return contents
    def get_chapter(self):
         req=requests.get(url=self.ip)
         html=req.text
         ss=BeautifulSoup(html,'lxml')
         mulu=ss.find_all(self.flag1,class_=self.flag1_class)
         mulu=BeautifulSoup(str(mulu[0]),'lxml')
         mulu=mulu.find_all(self.cara)
         chaptername=[]
         urls=[]
         for each in mulu[self.deleterow:]:
            chaptername.append(each.string)
            urls.append(self.ipplus + each.get('href'))
         return chaptername,urls
    def writer(self,chaptername,contents):
         with open(self.path,'a',encoding='utf-8') as f:
             f.write(chaptername +'\n')
             f.writelines(contents)
             f.write('\n\n')
    def run(self):
         chaptername,urls=self.get_chapter()
         print ("开始下载")
         for i in range(len(urls)):
            contents=self.get_contents(urls[i])
            name=chaptername[i]
            self.writer(name,contents)
         print ("下载完成")
