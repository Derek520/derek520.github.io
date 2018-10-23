---
layout: post
title: The operation couldn’t be completed. Unable to log in with account 
categories: Bug
description: The operation couldn’t be completed. Unable to log in with account 
keywords: iOS,错误,Bug
comments: true
---


# The operation couldn’t be completed. Unable to log in with account ''

作者:**AustinKuture**

```
摘要: 使用真机登陆时，若出现如下错误则说明账号已经过期，重新登陆开发者账号即可。
     errors：The operation couldn’t be completed. Unable to log in 
     with account 'myappleid'. An unexpected failure occurred while 
     logging in (Underlying error code 1100).
```

> 解决方法：打开Xcode 点击Preference->Accounts 点击你的开发账号，将登陆已经过期的账号重新登陆，然后重启Xcode即可。




