layout: post
title: HTML结构零散
keywords:
- HTML
categories:
- HTML
tags:
- HTML
toc: true
author: luuman
date: 2016-01-13 13:58:41
description:
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why
　　最近，使用Hexo遇到了很多问题，在设立进行整理。

<!-- more -->
## !DOCTYPE

### 版权声明



>XHTML

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" >
```

>HTML 5

```
<!-- HTML 5 -->
<!DOCTYPE html>
<html>
```

```
<!-- HTML 5 -->
<!DOCTYPE html>
<html lang='en' xmlns='http://www.w3.org/1999/xhtml'>
```
### 语言

```
<html lang='en' xmlns='http://www.w3.org/1999/xhtml'>
```

## HTML


## HEAD
<head>

### 标题

```
<!-- 标题 -->
<title>HTML Base</title>
```


### base默认地址

```
<base> 标签为页面上的所有链接规定默认地址或默认目标。
使用 <base> 标签可以改变这一点。
浏览器随后将不再使用当前文档的 URL，而使用指定的基本 URL 来解析所有的相对 URL。
这其中包括 <a>、<img>、<link>、<form> 标签中的 URL。
在 HTML 中，<base> 标签没有结束标签；在 XHTML 中，<base> 标签必须被正确地关闭。
但是还是建议要闭合标签，这样不同浏览器兼容不容。

```

```
该标签将会控制所有链接，围棋添加默认的链接。
默认的链接
<base href="http://www.w3school.com.cn/i/" />
默认的链接打开方式
<base target="_blank" />

注意：
通常通常情况下，默认链接会自动添加到链接的前面。但是，也有特例：
<base href="http://www.w3school.com.cn/i/" />
<link rel="stylesheet" href="css/root.css"/>
http://www.w3school.com.cn/i/css/root.css

但是，如果添加根目录（绝对路径），链接会自动根据默认链接进行根目录的查询指定。
<base href="http://www.w3school.com.cn/i/" />
<link rel="stylesheet" href="/css/root.css"/>
http://www.w3school.com.cn/css/root.css
```

### meta


#### 编码格式

```
<!-- 编码格式 -->
<meta charset="utf-8">
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
```
#### 编码格式

```
<meta http-equiv="X-UA-Compatible" content="IE=7">  
<!-- 指定网页的兼容性模式设置 -->

<meta http-equiv="X-UA-Compatible" content="IE=8">  
<!-- 以上代码告诉IE浏览器，无论是否用DTD声明文档标准，IE8/9都会以IE7引擎来渲染页面。   -->

<meta http-equiv="X-UA-Compatible" content="IE=edge">  
<!-- 以上代码告诉IE浏览器，IE8/9都会以IE8引擎来渲染页面。   -->

<meta http-equiv="X-UA-Compatible" content="IE=7,IE=9">  
<!-- 以上代码告诉IE浏览器，IE8/9及以后的版本都会以最高版本IE来渲染页面。   -->

<meta http-equiv="X-UA-Compatible" content="IE=7,9">  
<meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
<!-- 以上代码IE=edge告诉IE使用最新的引擎渲染网页，chrome=1则可以激活Chrome Frame. -->

#### 关键词

```
<!-- 关键词 -->
<meta name="keywords" content="" />
```
#### 描述

```
<!-- 描述 -->
<meta name="description" content="" />
```
#### 可视区域

```
<!-- 可视区域 -->
<meta name="viewport" content="width=device-width,height=device-height,initial-scale=1.0,maximum-scale=1.0,user-scalable=no">

width - viewport的宽度 
height - viewport的高度 
initial-scale - 初始的缩放比例 
minimum-scale - 允许用户缩放到的最小比例 
maximum-scale - 允许用户缩放到的最大比例 
user-scalable - 用户是否可以手动缩放 

```

#### 禁止了把数字转化为拨号链接

```
<!-- 禁止了把数字转化为拨号链接 -->
<meta name="format-detection" content="telephone=no" />
```

#### 关键词

```
<!-- 删除默认的苹果工具栏和菜单栏 -->
<meta name="apple-mobile-web-app-capable" content="yes" />
```

#### 关键词

```
<!-- 控制状态栏显示样式 -->
<meta name="apple-mobile-web-app-status-bar-style" content="default" />
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />

默认：default（白色）
black（黑色）
black-translucent（灰色半透明）
```
#### iphone的safari浏览器

```
<!-- iphone的safari浏览器 -->
<meta name="apple-itunes-app" content="app-id=432274380" />
<!-- <meta name="znonce" content="74810a1113ff4cf49d97f2616bdfe158"> -->
```

#### 访问时以兼容模式访问

```
<!-- 访问时以兼容模式访问 -->

<!-- 默认webkit内核 -->
<meta name="renderer" content="webkit">
<!-- 默认IE兼容模式 -->
<meta name="renderer" content="ie-comp">
<!-- 默认IE标准模式 -->
<meta name="renderer" content="ie-stand">
```
#### 添加Meta声明

```
<!-- 用于添加Meta声明；无对应关系的PC页面无需添加Meta -->
<meta http-equiv="mobile-agent" content="format=[wml|xhtml|html5]; url=url">
<meta http-equiv="mobile-agent" content="format=html5;url=http://www.z.com/">
```
#### 网站所有者

```
<!-- 验证网站所有者的一种方式 -->
<meta property="wb:webmaster" content="8e9c4b702508b902" />
```
### 引入link

#### Icon link

```
<!-- Icon link -->
<link rel="shortcut icon" href="favicon.ico">
<!-- 添加到主屏上的图标会使用指定的图片 -->
<link rel="apple-touch-icon" href="templets/default/images/ico/apple-touch-icon.png">
<!-- ipad -->
<link rel="apple-touch-icon" sizes="72x72" href="templets/default/images/ico/apple-touch-icon-72.png">
<!-- iPhone、iTouch -->
<link rel="apple-touch-icon" sizes="114x114" href="templets/default/images/ico/apple-touch-icon-114.png">

<!-- precomposed -->
<link rel="apple-touch-icon-precomposed" href="static/img/ios/zhihu(57px).png" />
<link rel="apple-touch-icon-precomposed" sizes="72x72" href="templets/default/images/ico/apple-touch-icon-72.png">
<link rel="apple-touch-icon-precomposed" sizes="114x114" href="templets/default/images/ico/apple-touch-icon-114.png">
```
#### section

```
<!-- 把搜索功能放到浏览器的快捷搜索工具上 -->
<link rel="search" type="application/opensearchdescription+xml" href="static/search.xml" title="知乎" />
```
#### section

```
<link rel="stylesheet" href=".css">
```
### 引入JavaScript

```
<!-- JavaScript -->
<script type="text/javascript"></script>
```

### 引入style

```
<style>
</style>
```
### hack IE
用于解决IE兼容性问题的特殊方案，只有满足条件，才会执行代码，否则视为注释。

```
<!-- hack IE -->
<!--[if lt IE 9]>
<script src="http://cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
<![endif]-->
```
</head>

## Body


<body>

>audio声音事件
[美团外卖商家中心](http://e.waimai.meituan.com/#/v2/order/pre)

```
<audio id="main_audio" preload="auto" volume="1.0" loop
data-type="waimai">
<source src="meituan://waimai.ogg" type="audio/ogg"/>
<source src="static/media/waimai.ogg" type="audio/ogg"/>
</audio>
<!-- 加入refundloop的判断 -->
<audio id="refund-audio" preload="auto" volume="1.0" 
data-type="one">
<source src="meituan://refund.ogg" type="audio/ogg"/>
<source src="static/media/refund.ogg" type="audio/ogg"/>
</audio>
```

</body>
</html>

# CSS

iframe无法全屏显示，html，设置高度100%。


CSS a标签，移动端显示方框


.f-img-light-wrap {
	overflow: hidden;
	position: relative
}

.f-img-light-wrap:after {
	content: '';
	height: 100%;
	width: 100px;
	transform: skewX(-25deg) translate3d(0,0,0);
	background: -moz-linear-gradient(left,rgba(255,255,255,0) 0,rgba(255,255,255,.3) 50%,rgba(255,255,255,0) 100%);
	background: -webkit-gradient(linear,left top,right top,color-stop(0%,rgba(255,255,255,0)),color-stop(50%,rgba(255,255,255,.3)),color-stop(100%,rgba(255,255,255,0)));
	background: -webkit-linear-gradient(left,rgba(255,255,255,0) 0,rgba(255,255,255,.3) 50%,rgba(255,255,255,0) 100%);
	background: -o-linear-gradient(left,rgba(255,255,255,0) 0,rgba(255,255,255,.3)50%,rgba(255,255,255,0) 100%);
	background: linear-gradient(left,rgba(255,255,255,0) 0,rgba(255,255,255,.3) 50%,rgba(255,255,255,0) 100%);
	position: absolute;
	left: -160%;
	top: 0;
	z-index: 9
}

.f-img-light-wrap:hover:after {
	transition: left 1s ease-in-out;
	left: 160%
}



	/*首字母大写*/
	text-transform:capitalize;











<iframe src="http://sandbox.runjs.cn/show_square/587" allowtransparency="true" frameborder="0" scrolling="no" style=""></iframe>