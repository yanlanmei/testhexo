title: Js-Rem的理解
date: 2016-04-02 14:11:20
description: 
categories:
- HTML
tags:
- rem
toc: true
author:
comments:
original:
permalink: 
---

　　**：**

<!-- more -->

### Boss直聘[Js-Rem](http://m.bosszhipin.com/share/boss/40c5dca696f24efa0XR62Nu7Eg~~ "李焰 提谱旅行.运营")

类似百度的自适应跳转，但是将font-size限制在40px之内。

```
(function(doc,win){
  var docEl = doc.documentElement,
  recalc = function(){
    var clientWidth = docEl.clientWidth;
    if(!clientWidth){return}
    var w = 20 * (clientWidth / 320);
    if(w > 40){
      w = 40;
    }
    docEl.style.fontSize = w + "px";
  };
if(!doc.addEventListener){return}
if("orientationchange" in window){
  win.addEventListener("orientationchange",recalc,false)
}
win.addEventListener("resize",recalc,false);
win.addEventListener("load",recalc,false);
doc.addEventListener("DOMContentLoaded",recalc,false);
recalc();
})(document,window);
```

```
font-size:20px

4.5rem = 90px

.kz_dflex{
  display: -webkit-flex;
  display: -ms-flexbox;
  display: -webkit-box;
  display: -moz-box;
  display: flex;
}

.kz_flex{
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
}

```

### 百度[Js-Rem](http://waimai.baidu.com/mobile/waimai?qt=confirmcity&third_party=0 "百度外卖")

```
(function(doc,win){
	var docEl = doc.documentElement,
	resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
	recalc = function(){
		var clientWidth = docEl.clientWidth;
		if(!clientWidth) return;
		docEl.style.fontSize = 20 * (clientWidth / 320) + 'px';
	};
	if(!doc.addEventListener) return;
	win.addEventListener(resizeEvt,recalc,false);
	doc.addEventListener('DOMContentLoaded',recalc,false);
})(document,window);
```

### 五谷[Js-Rem]()

网上一个朋友公司的自适应效果，font-size效果太局限了。

```
$(function() {
	$(window).resize(infinite);
	function infinite() {
		var htmlWidth = $('html').width();
		if (htmlWidth >= 1080) {
			$("html").css({
				"font-size" : "42px"
			});
		} else {
			$("html").css({
				"font-size" : 42 / 1080 * htmlWidth + "px"
			});
		}
	}
	infinite();
});

```

### [Js-Rem]()

```
console.time("test");
/*
    # 按照宽高比例设定html字体, width=device-width initial-scale=1版
    # @pargam win 窗口window对象
    # @pargam option{
      designWidth: 设计稿宽度，必须
      designHeight: 设计稿高度，不传的话则比例按照宽度来计算，可选
      designFontSize: 设计稿宽高下用于计算的字体大小，默认20，可选
      callback: 字体计算之后的回调函数，可选
    }
    # return Boolean;
    # xiaoweili@tencent.com
    # ps:请尽量第一时间运行此js计算字体
*/
!function(win, option) {
  var count = 0, 
      designWidth = option.designWidth, 
      designHeight = option.designHeight || 0, 
      designFontSize = option.designFontSize || 20, 
      callback = option.callback || null,
      root = document.documentElement,
      body = document.body,
      rootWidth, newSize, t, self;
      root.style.width = 100 + "%";
  //返回root元素字体计算结果
  function _getNewFontSize() {
    var scale = designHeight !== 0 ? Math.min(win.innerWidth / designWidth, win.innerHeight / designHeight) : win.innerWidth / designWidth;
    return parseInt( scale * 10000 * designFontSize ) / 10000;
  }
  !function () {
    rootWidth = root.getBoundingClientRect().width;
    self = self ? self : arguments.callee;
    //如果此时屏幕宽度不准确，就尝试再次获取分辨率，只尝试20次，否则使用win.innerWidth计算
    if( rootWidth !== win.innerWidth &&  count < 20 ) {
      win.setTimeout(function () {
        count++;
        self();
      }, 0);
    } else {
      newSize = _getNewFontSize();
      //如果css已经兼容当前分辨率就不管了
      if( newSize + 'px' !== getComputedStyle(root)['font-size'] ) {
        root.style.fontSize = newSize + "px";
        return callback && callback(newSize);
      };
    };
  }();
  //横竖屏切换的时候改变fontSize，根据需要选择使用
  win.addEventListener("onorientationchange" in window ? "orientationchange" : "resize", function() {
    clearTimeout(t);
    t = setTimeout(function () {
      self();
    }, 300);
  }, false);
}(window, {
  designWidth: 640, 
  designHeight: 1136,
  designFontSize: 20,
  callback: function (argument) {
    console.timeEnd("test")
  }
});
```