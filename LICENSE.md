# -*- coding:utf-8 -*-
import urllib
import urllib2
import re

page = raw_input("pages?>")
url = 'http://www.qiushibaike.com/hot/page/' + str(page)
user_agent = 'Mozilla/5.0 (Windows NT 6.1; WOW64)'
headers = {'User-Agent' : user_agent}
try:
    request = urllib2.Request(url,headers = headers)
    response = urllib2.urlopen(request)
    content = response.read().decode('utf-8')
    pattern = re.compile('<div class="content">.*?<span>(.*?)</span>',re.S)
    items = re.findall(pattern,content)
    for item in items:
        print item
        print ""
except urllib2.URLError,e:
    if hasattr(e,"code"):
        print e.code
    if hasattr(e,"reason"):
        print e.reason
