---
layout: post
title: xpath 和 jsonpath对比
categories: Spider
description: xpath 和 jsonpath对比
keywords: Spider
comments: true
---


摘要： JsonPath与XPath语法对比，介绍在使用中语法差别，以及使用方法，简单代码示例

Json结构清晰，可读性高，复杂度低，非常容易匹配，下表中对应了XPath的用法。

| XPath | JSONPath | 描述 |
| :--- | :--- | :--- |
| `/` | `$` | 根节点 |
| `.` | `@` | 现行节点 |
| `/` | `.`or`[]` | 取子节点 |
| `..` | n/a | 取父节点，Jsonpath未支持 |
| `//` | `..` | 就是不管位置，选择所有符合条件的条件 |
| `*` | `*` | 匹配所有元素节点 |
| `@` | n/a | 根据属性访问，Json不支持，因为Json是个Key-value递归结构，不需要属性访问。 |
| `[]` | `[]` | 迭代器标示（可以在里边做简单的迭代操作，如数组下标，根据内容选值等） |
| \| | `[,]` | 支持迭代器中做多选。 |
| `[]` | `?()` | 支持过滤操作. |
| n/a | `()` | 支持表达式计算 |
| `()` | n/a | 分组，JsonPath不支持 |

```
import requests,json
from jsonpath import jsonpath
from User_agent import User_Agt

url = 'http://www.lagou.com/lbs/getAllCitySearchLabels.json'
headers = User_Agt()
res = requests.get(url,headers=headers)
str_data = res.content.decode()

json_data = json.loads(str_data)

print(json_data)

# 这句意思，就是不管nana在什么位置，凡是有的都会查到
js_data = jsonpath(json_data,'$..name')

print(js_data)
```

###Xpath基本使用

starts-with 顾名思义，匹配一个属性开始位置的关键字

contains 匹配一个属性值中包含的字符串

text（） 匹配的是显示文本信息，此处也可以用来做定位用


//input\[starts-with\(@name,'name1'\)\]     查找name属性中开始位置包含'name1'关键字的页面元素

//input\[contains\(@name,'na'\)\]         查找name属性中包含na关键字的页面元素

&lt;a href="http://www.baidu.com"&gt;百度搜索&lt;/a&gt;

xpath写法为 //a\[text\(\)='百度搜索'\] 

或者 //a\[contains\(text\(\),"百度搜索"\)\]
