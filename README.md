
Python+selenium+PhontomJS完成爬虫
====
# 环境搭建
准备工具：python3.6, selenium, PhantomJS
安装selenium：
''' python
! pip install selenium
'''
安装PhantomJS:
按照系统环境下载[phantomjs]('http://phantomjs.org/'),将phantomjs.exe解压到python的script文件夹下。

# 使用selenium+phantomjs实现简单爬虫
''' python
from selenium import webdriver
driver = webdriver.PhantomJS()
driver.get('http://www.baidu.com')  # 加载网页
data = driver.page_source  # 获取网页文本
driver.save_screenshot('1.png')  # 截图保存
print(data)
driver.quit()
'''
