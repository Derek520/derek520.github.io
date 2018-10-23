---
layout: post
title: Selenium和PhantomJS
categories: Spider
description: Selenium和PhantomJS
keywords: Spider
comments: true
---

摘要：在抓取数据中遇到的动态页面，js加载的数据解决方法，selenium的使用方法，以及如何使用cookie，使用场景附带代码实例

### 加载动态网页：
```angular2html

from selenium import webdriver
driver = webdriver.PhantomJS\(“c:…/pantomjs.exe”\)
driver.get\("[http://www.baidu.com/](http://www.baidu.com/)"\)
driver.save\_screenshot\("长城.png"\)

```
```
#coding=utf-8
from selenium import webdriver
import time


#实例化得到driver
driver = webdriver.Chrome()
# driver = webdriver.PhantomJS()

#设置窗口size
# driver.set_window_size(1920,1080)
#最大化窗口
# driver.maximize_window()

#请求百度
# driver.get("https://movie.douban.com/")
driver.get("http://www.baidu.com")
#driver定位元素
driver.find_element_by_id("kw").send_keys("传智播客") #输入值
driver.find_element_by_id("su").click() #点击

#获取网页源码
# print(driver.page_source)

# print(driver.current_url)

print(driver.get_cookies())
cookie_dict = {i["name"]:i["value"] for i in driver.get_cookies()}
print(cookie_dict)

#截图
# driver.save_screenshot("./baidu.png")

#退出
time.sleep(5)
driver.quit()
```

### 定位和操作：

driver.find\_element\_by\_id\(“kw”\).send\_keys\(“长城”\)
driver.find\_element\_by\_id\("su"\).click\(\)

### 查看请求信息：

driver.page\_source
driver.get\_cookies\(\)
driver.current\_url

### 退出

driver.close\(\) \#退出当前页面
driver.quit\(\) \#退出浏览器

## 页面元素定位

### 用法：

find\_element\_by\_id \(返回一个\)
find\_elements\_by\_xpath （返回一个列表）
find\_elements\_by\_link\_text
find\_elements\_by\_partial\_link\_text
find\_elements\_by\_tag\_name
find\_elements\_by\_class\_name
find\_elements\_by\_css\_selector

### 注意点:

find\_element 和find\_elements的区别：返回一个和返回一个列表
by\_link\_text和by\_partial\_link\_text的区别：全部文本和包含某个文本
by\_css\_selector的用法： \#food span.dairy.aged
by\_xpath中获取属性和文本需要使用get\_attribute\(\) 和.text

```
from selenium import webdriver

driver =webdriver.Chrome()

# driver.get("https://npm.taobao.org/mirrors/chromedriver")
driver.get("https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=%E6%B7%98%E5%AE%9D%E9%95%9C%E5%83%8F&oq=exec%2520format%2520error%253A%2520chromedriver&rsv_pq=e03471a70000bf00&rsv_t=8feaYZYpC%2FqnsFJkn%2FmHaK%2FeIm%2FNqHVWai5%2Bqa0iATAHYyN2D6U4WrUVRQw&rqlang=cn&rsv_enter=1&inputT=823&rsv_sug3=41&rsv_sug1=28&rsv_sug7=100&bs=exec%20format%20error%3A%20chromedriver")

#xpath的使用
ret = driver.find_elements_by_xpath("//preerewr/a")
# for a in ret:
# print(a.get_attribute("href"),"----",a.text)
# print(ret)

#类名
# div_list= driver.find_elements_by_class_name("question-summary")
# for div in div_list:
# div.fin

#标签的文本
# ret = driver.find_element_by_link_text("下一页>").get_attribute("href")
# ret = driver.find_element_by_partial_link_text("下一页").get_attribute("href")


print(ret)

driver.quit()from selenium import webdriver

driver =webdriver.Chrome()

# driver.get("https://npm.taobao.org/mirrors/chromedriver")
driver.get("https://www.baidu.com/s?ie=utf-8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=%E6%B7%98%E5%AE%9D%E9%95%9C%E5%83%8F&oq=exec%2520format%2520error%253A%2520chromedriver&rsv_pq=e03471a70000bf00&rsv_t=8feaYZYpC%2FqnsFJkn%2FmHaK%2FeIm%2FNqHVWai5%2Bqa0iATAHYyN2D6U4WrUVRQw&rqlang=cn&rsv_enter=1&inputT=823&rsv_sug3=41&rsv_sug1=28&rsv_sug7=100&bs=exec%20format%20error%3A%20chromedriver")

#xpath的使用
ret = driver.find_elements_by_xpath("//preerewr/a")
# for a in ret:
    # print(a.get_attribute("href"),"----",a.text)
    # print(ret)

#类名
# div_list= driver.find_elements_by_class_name("question-summary")
# for div in div_list:
    # div.fin

#标签的文本
# ret = driver.find_element_by_link_text("下一页>").get_attribute("href")
# ret = driver.find_element_by_partial_link_text("下一页").get_attribute("href")


print(ret)

driver.quit()
```

## cookie

### Cookie相关用法：

{cookie\[‘name’\]: cookie\[‘value’\] for cookie in driver.get\_cookies\(\)}
driver.delete\_cookie\("CookieName"\)
driver.delete\_all\_cookies\(\)

## Selenium总结

#### 应用场景：

* 动态html页面请求
* 登录获取cookies
#### 如何使用
* 导包并且实例化driver
* 发送请求
* 定位获取数据
* 保存
* 退出driver
#### Cookies相关方法：
* get\_cookies\(\)
#### 页面等待
* 强制等待

### selenium常见异常

1.NoSuchElementException：没有找到元素

2.NoSuchFrameException：没有找到iframe

3.NoSuchWindowException:没找到窗口句柄handle

4.NoSuchAttributeException:属性错误

5.NoAlertPresentException：没找到alert弹出框

6.lementNotVisibleException：元素不可见

7.ElementNotSelectableException：元素没有被选中

8.TimeoutException：查找元素超时

9.StaleElementReferenceException :解析元素失败

### 访问嵌套访问的方法和cookies

```
# -*- coding:utf-8 -*-
import requests
from selenium import webdriver
import time
driver = webdriver.Chrome()


"""
form_email
form_password
bn-submit
"""
# driver.get("https://www.douban.com/")
#
# driver.find_element_by_id("form_email").send_keys("yuanyulong")
#
# driver.find_element_by_id("form_password").send_keys("123456")
#
# driver.find_element_by_class_name("bn-submit").click()
#
# time.sleep(10)

driver.get("https://mail.qq.com/")

# 访问网页嵌套网页访问方式
driver.switch_to.frame("login_frame")

driver.find_element_by_id("u").send_keys("502440711")
driver.find_element_by_id('p').send_keys("yuan121423")
driver.find_element_by_id("login_button").click()

# 获取cookies
cookie_list = [{i["name"]:i["value"]}for i in driver.get_cookies()]
print(cookie_list)


time.sleep(10)
```


