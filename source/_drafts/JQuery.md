title: JQuery学习计划
date: 2015-12-25 18:29:00
description: 
categories:
- HTML
tags:
- JQuery
toc: true
author:
comments:
original:
permalink: 
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why
<!-- more -->


## function

$(window).load(function(){}
$(window).on('load', function(){}


[]( "")



console.log("左面" + "天");
## jquery如何判断checkbox（复选框）是否被选中

jquery alert($("#id").attr("checked")) 会提示您是true而不是checked
```

## 在文档加载后激活函数：
$(document).ready(function() {});



## 样式的设置

$("#ID").css("style","style")
$("#ID").css("style":"style","style":"style","style":"style")
$(".ActDay").css({"margin":"1rem 50%","transform":"translatex(-50%)"});