
Python+selenium+PhontomJS完成爬虫
====
# 环境搭建
准备工具：python3.6, selenium, PhantomJS
安装selenium：
```Python
  ! pip install selenium
```

安装PhantomJS:
按照系统环境下载[phantomjs](http://phantomjs.org/),将phantomjs.exe解压到python的script文件夹下。

# 使用selenium+phantomjs实现简单爬虫
``` python
from selenium import webdriver
driver = webdriver.PhantomJS()
driver.get('http://www.baidu.com')  # 加载网页
data = driver.page_source  # 获取网页文本
driver.save_screenshot('1.png')  # 截图保存
print(data)
driver.quit()
```

# selenium+phantomjs的一些使用方法
## 设置请求头里的user-Agent
```python
from selenium import webdriver
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities
dcap = dict(DesiredCapabilities.PHANTOMJS)  #设置useragent
dcap['phantomjs.page.settings.userAgent'] = ('Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:25.0) Gecko/20100101 Firefox/25.0 ')  #根据需要设置具体的浏览器信息
driver = webdriver.PhantomJS(desired_capabilities=dcap)  #封装浏览器信息
driver.get('http://www.baidu.com')   #加载网页
data = driver.page_source   #获取网页文本
driver.save_screenshot('1.png')   #截图保存
print(data)
driver.quit()
```

## 请求超时设置
**webdriver类中有三个和时间相关的方法：**

1.PageLoadTimeout 设置页面完全加载的超时时间，完全加载即完全渲染完成，同步和异步脚本都执行完

2.setScriptTimeout 设置异步脚步的超时时间

3.implicitlyWait 识别对象的智能等待时间

```python
from selenium import webdriver
driver = webdriver.PhantomJS()
driver.set_page_load_timeout(5)  #设置超时时间
print(driver.title)
driver.quit()
```

# 设置浏览器窗口大小
调用启动的浏览器不是全屏的，有时会影响我们的某些操作，所以我们可以设置全屏
```python
driver.maximize_windows() #设置全屏
driver.set_window_size('480','800') #设置浏览器宽480,高800
```

# 元素定位
```python
from selenium import webdriver
driver = webdriver.PhantomJS()
driver.set_page_load_timeout(5)
driver.get('http://www.baidu.com')
try:
    driver.get('http://www.baidu.com')
    driver.find_element_by_id('kw')  #通过ID定位
    driver.find_element_by_class_name('s_ipt')  #通过class属性定位
    driver.find_element_by_name('wd')  #通过标签name属性定位
    driver.find_element_by_tag_name('input')  #通过标签属性定位
    driver.find_element_by_css_selector('#kw')  #通过css方式定位
    driver.find_element_by_xpath('//input[@id='kw']')  #通过xpath方式定位
    drivrt.find_element_by_link_text('贴吧')  #通过xpath方式定定位
    print(driver.find_element_by_id('kw').tag_name)  #获取标签的类型
   except Exception as e:
       print(e)
   driver.quit()
```

# 操作浏览器前进或后退
```python
from selenium import webdriver
driver = webdriver.PhantomJS()
try:
    driver.get('http://www.baidu.com')   #访问百度首页
    driver.save_screenshot('1.png')
    driver.get('http://www.sina.com.cn') #访问新浪首页
    driver.save_screenshot('2.png')
    driver.back()                           #回退到百度首页
    driver.save_screenshot('3.png')
    driver.forward()                        #前进到新浪首页
    driver.save_screenshot('4.png')
except Exception as e:
    print(e)
driver.quit()
```
