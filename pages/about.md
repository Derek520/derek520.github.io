---
layout: page
title: About
description: 书从疑处翻成悟，文到穷时自有神
keywords: Derek,Derek520,yulong,袁宇龙
comments: true
menu: 关于
permalink: /about/
---

书从疑处翻成悟，

文到穷时自有神.



## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}




{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
