---
layout: post
title: GitBook报错is not a recognized liquid tag
categories:
  - Bug
description: GitBook报错is not a recognized liquid tag
keywords: gitbook,liquid tag
comments: true
---

# GitBook报错is not a recognized liquid tag

使用gitbook编写博客上传时报错’...is not a recognized liquid tag‘，其主要原因是文章中包含html代码。Gitpage对md与html是通用的，当md文件中包含html代码进就会因为格式异常而报错。
### [解决办法](#)
#### 方法一：

将要展示的html代码以图片的形式进行替换

#### 方法二：
 
html代码首尾加上标识语言

![LiquidTag](/images/posts/Bug/liquidtag00.png)

效果如下所示：

{% highlight html linenos %}
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
    </body>
</html>
{% endhighlight %}


