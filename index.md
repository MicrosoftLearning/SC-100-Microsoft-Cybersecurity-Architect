---
title: Online Hosted Instructions
permalink: index.html
layout: home
---

# Content Directory

Hyperlinks to each case study is listed below.


## CaseStudy

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudy'" %}
| Module | CaseStudy |
| --- | --- | 
{% for activity in casestudy  %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
