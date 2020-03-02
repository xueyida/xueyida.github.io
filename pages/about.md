---
layout: page
title: About
description: 打码改变世界
keywords: About 
comments: true
menu: 关于
permalink: /about/
---

未知人生不低头

渐行渐远不回首

或道求索遥遥遥遥期

形单影只慢慢行


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
