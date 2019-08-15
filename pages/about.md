---
layout: page
title: About
description: 
keywords: Commando, 黄亮
comments: true
menu: 关于
permalink: /about/
---

我是黄亮。

人生是一个舞台，每个人都在真实的演出。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
