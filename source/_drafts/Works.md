title: 移动端 h5开发相关内容总结——CSS篇
date: 2015-12-25 18:29:00
description: 
categories:
- 微信
tags:
- 微信
toc: true
author:
comments:
original:
permalink: 
---
　　**微信网页开发：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why
<!-- more -->

### 自动刷新

```
//指定15秒刷新一次
setTimeout('window.location.reload();',120000);
```

### 旅游信息页面

```
id 页面ID

//旅游信息页面
function appshares(id) {
    try{
        UserModel.scenicInfo(id);
    }catch(error){
            window.location.href="http://a.app.qq.com/o/simple.jsp?pkgname=com.jingqubao.tips"
        }finally{
    } 
}
```

### 旅图发布

```
//旅图发布
function appshare() {
    try{
        UserModel.publishTravelPhoto("");
    }catch(error){
            window.location.href="http://a.app.qq.com/o/simple.jsp?pkgname=com.jingqubao.tips"
        }finally{
    }
}
```

### 移动端Active激活

```
document.addEventListener("touchstart", function(){
}, true);
```

### 判断移动设备

```
//判断移动设备
var u = navigator.userAgent;
var URLs = "";
var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1; //android终端
var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
if(isAndroid){
    URLs = "send_travel_photo_from_android";
}else if(isiOS){
    URLs = "send_travel_photo_from_ios";
}
```

### 浏览器版本信息

```
function browser() {
    var u = navigator.userAgent.toLowerCase();
    var app = navigator.appVersion.toLowerCase();
    return {
        txt: u, // 浏览器版本信息
        version: (u.match(/.+(?:rv|it|ra|ie)[\/: ]([\d.]+)/) || [])[1], // 版本号       
        msie: /msie/.test(u) && !/opera/.test(u), // IE内核
        mozilla: /mozilla/.test(u) && !/(compatible|webkit)/.test(u), // 火狐浏览器
        safari: /safari/.test(u) && !/chrome/.test(u), //是否为safair
        chrome: /chrome/.test(u), //是否为chrome
        opera: /opera/.test(u), //是否为oprea
        presto: u.indexOf('presto/') > -1, //opera内核
        webKit: u.indexOf('applewebkit/') > -1, //苹果、谷歌内核
        gecko: u.indexOf('gecko/') > -1 && u.indexOf('khtml') == -1, //火狐内核
        mobile: !!u.match(/applewebkit.*mobile.*/), //是否为移动终端
        ios: !!u.match(/\(i[^;]+;( u;)? cpu.+mac os x/), //ios终端
        android: u.indexOf('android') > -1, //android终端
        iPhone: u.indexOf('iphone') > -1, //是否为iPhone
        iPad: u.indexOf('ipad') > -1, //是否iPad
        webApp: !!u.match(/applewebkit.*mobile.*/) && u.indexOf('safari/') == -1 //是否web应该程序，没有头部与底部
    };
}
browser();
```

### LoadingBar页面顶部加载进度条

```
<link href="css/pace/pace-theme-flash.css" rel="stylesheet" />
<!-- loading -->
<script src="js/pace.min.js"></script>
```


### 介绍

```
<link rel="stylesheet" type="text/css" media="screen and (max-width:819px)" href="css/index_s.css"/>
```
 



### 介绍

```
```