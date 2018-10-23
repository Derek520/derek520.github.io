---
layout: post
title: AFN NSURLSession/NSURLConnection HTTP load failed (kCFStreamErrorDomainSSL, -9806)
categories: Bug
description: AFN NSURLSession/NSURLConnection HTTP load failed (kCFStreamErrorDomainSSL, -9806)
keywords: AFN,-9806,HTTP load failed
comments: true
---


# AFN NSURLSession/NSURLConnection HTTP load failed (kCFStreamErrorDomainSSL, -9806)

作者: **AustinKuture**

```
摘要: 使用AFNetworking请求https链接的数据时,
     报错NSURLSession/NSURLConnection HTTP load failed 
     (kCFStreamErrorDomainSSL, -9806),其原因主要是加密协议版本不...
```

## 一,  加密协议不统一

iOS 9之后默认的加密协议是TLSv1.2,目前有些服务端仍然使用的是TLSv1.0,这样就会因为协议不统一而造成应用端与服务端不能建立连接,并报错:`Error Domain=NSURLErrorDomain Code=-1200`

- 解决方法有两种:

  - 第一种方法 : 从应用端修改

    右击plist文件 -> Open As -> Source Code,在其中加入如下代码:                   

    ```
      <key>域名</key>  
      <dict>
        <key>NSIncludesSubdomains</key>
        <true/>
        <key>NSThirdPartyExceptionAllowsInsecureHTTPLoads</key>
        <true/>
        <key>NSExceptionMinimumTLSVersion</key>
        <string>TLSv1.0</string>
        <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
        <false/>
      </dict>
    ```

  - 第二种方法 : 从服务端修改

    让服务端将加密协议从TLSv1.0或者TLSv1.1改为TLSv1.2       

## 二, 服务端使用了签名证书

- 服务端如果使用了未经第三方机构认证的证书,使用afn请求数据时会报错:NSURLSession/NSURLConnection HTTP load failed (kCFStreamErrorDomainSSL, -9806)

- 将服务端的三个证书,选择其中一个(例如.crt或者.pem)放在本地双击打开会被添加到钥匙串,从钥匙串导出后缀为.cer的文件,然后拖入到项目中. 打开 Build Phases -> Copy Bunld Resources 查看证书是否已经绑定,如果没有点击 + 号绑定证书.完成后,在请求数据的地方加入Security的设置:

  ```
  AFSecurityPolicy * securityPolicy  = [AFSecurityPolicypolicyWithPinningMode:AFSSLPinningModeCertificate];  
      securityPolicy.allowInvalidCertificates = YES;  
      securityPolicy.validatesDomainName = NO;  
      manager.securityPolicy = securityPolicy; 
  ```

完成后,重新运行即可.