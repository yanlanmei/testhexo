title: JS学习计划
date: 2015-12-25 18:29:00
description: 
categories:
- HTML
tags:
- CSS
toc: true
author:
comments:
original:
permalink: 
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why
<!-- more -->
[]()

## CSS动画

### transition

Internet Explorer 9 以及更早版本的浏览器不支持 transition 属性

transition 属性是一个简写属性，用于设置四个过渡属性：

* transition-property	规定设置过渡效果的 CSS 属性的名称。
* transition-duration	规定完成过渡效果需要多少秒或毫秒。
* transition-timing-function	规定速度效果的速度曲线。
* transition-delay	定义过渡效果何时开始。

```
-webkit-transition-duration: 0.5s;
transition-duration: 0.5s;

transition: property duration timing-function delay;

transition:width 2s;
/* Firefox 4 */
-moz-transition:width 2s; 
/* Safari and Chrome */
-webkit-transition:width 2s; 
/* Opera */
-o-transition:width 2s; 
```