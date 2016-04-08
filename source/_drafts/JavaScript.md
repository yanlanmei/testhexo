title: JavaScript学习计划
date: 2015-12-25 18:29:00
description: 
categories:
- HTML
tags:
- JavaScript
toc: true
author:
comments:
original:
permalink: 
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。在此记录自己已理解并开始遵循的前端代码规范。What How Why
<!-- more -->

## 属性的编辑方法

//方法一
oTxt.value = 'adjljl';

//方法二
oTxt['value'] = 'adjljl';

var a = 'value'
oTxt[a] = 'adjljl';
[]()

## 元素到屏幕的距离

### offsetLeft

```
var x=document.getElementById("x");

//到屏幕左边的距离
x.offsetLeft;

//到屏幕上边的距离
x.offsetTop;
```

## 滚动条

```
//IE
document.documentElement.scrollTop

//Chrome
document.body.scrollTop;
```

### 拓展：

```
网页可见区域宽： document.body.clientWidth;
网页可见区域高： document.body.clientHeight;
网页可见区域宽： document.body.offsetWidth (包括边线的宽);
网页可见区域高： document.body.offsetHeight (包括边线的宽);
网页正文全文宽： document.body.scrollWidth;
网页正文全文高： document.body.scrollHeight;
网页被卷去的高： document.body.scrollTop;
网页被卷去的左： document.body.scrollLeft;
网页正文部分上： window.screenTop;
网页正文部分左： window.screenLeft;
屏幕分辨率的高： window.screen.height;
屏幕分辨率的宽： window.screen.width;
屏幕可用工作区高度： window.screen.availHeight;
屏幕可用工作区宽度：window.screen.availWidth;


scrollHeight: 获取对象的滚动高度。 
scrollLeft:设置或获取位于对象左边界和窗口中目前可见内容的最左端之间的距离
scrollTop:设置或获取位于对象最顶端和窗口中可见内容的最顶端之间的距离
scrollWidth:获取对象的滚动宽度
offsetHeight:获取对象相对于版面或由父坐标 offsetParent 属性指定的父坐标的高度
offsetLeft:获取对象相对于版面或由 offsetParent 属性指定的父坐标的计算左侧位置
offsetTop:获取对象相对于版面或由 offsetTop 属性指定的父坐标的计算顶端位置 
event.clientX 相对文档的水平座标
event.clientY 相对文档的垂直座标

event.offsetX 相对容器的水平坐标
event.offsetY 相对容器的垂直坐标 
document.documentElement.scrollTop 垂直方向滚动的值
event.clientX+document.documentElement.scrollTop 相对文档的水平座标+垂直方向滚动的量
```

## window

### window.onload

```
//页面加载完毕，后触函数
window.onload = function(){}

window.onload事件只能有一个，如果有多个，则值运行最下面的那一个。

window.onload = function() {
    console.log("window.onload fn1");
}
window.onload = function() {
    console.log("window.onload fn2");
}

//jQuery代码
$(window).load(function(){})

具体区别还在研究当中，让我们来看看几种方法的整体效果：

jQuery(function() {
    console.log("jQuery fn1");
});
jQuery(function() {
    console.log("jQuery fn2");
});
$(document).ready(function() {
 console.log("$ fn2");
});
$(document).ready(function() {
    console.log("$ fn1");
});
window.onload = function() {
    console.log("window.onload fn1");
}
window.onload = function() {
    console.log("window.onload fn2");
}
```

### jQuery代码

```
//jQuery代码
$(window).load(function(){});

//在DOM完全就绪时就可以被调用
$(document).ready(function() {});
jQuery的ready()耗时 : 1365 ms
$(document).ready()方法是事件模块中最重要的一个函数，可以极大地提高Web应用程序的响应速度。

简写方式：

$(window).load(function(){}) 

等价于JavaScript中的以下代码：
window.onload = function(){})

上面我们ready函数写成这样：
$(document).ready(function(){})

也可以简写成这样：
$(function(){})

另外，$(document)也可以简写为$()。当$()不带参数时，默认参数就是“document”，因此可以简写为：
$().ready(function(){})

3种方式都是一样的功能，读者可以根据自己的喜好，选择其中的一种。
```

```
具体区别还在研究当中，让我们来看看几种方法的整体效果：

jQuery(function() {
    console.log("jQuery fn1");
});
jQuery(function() {
    console.log("jQuery fn2");
});
$(document).ready(function() {
 console.log("$ fn2");
});
$(document).ready(function() {
    console.log("$ fn1");
});
window.onload = function() {
    console.log("window.onload fn1");
}
window.onload = function() {
    console.log("window.onload fn2");
}
```



## 全局变量与局部变量

全局变量：
局部变量：

```
实例：

//全局变量：任何地方都可以使用
var n= 10; m= 10;

function demo(){

    //局部变量：只能在当前函数中使用
    var i = 10;

    //全局变量：任何地方都可以使用
    x = 10;
    alert(i);
}
demo();
alert(n);
```

## 对象


```
//创建对象
people = new Object();
people = {name:"iwen",age:"30"};


//创建属性
people.name = "luuman";
people.age = "20";

//创建函数对象
function people(name,age){
    this.name = name;
    this.age = age;
}
son = new people("wen",10);
document.write("name"+son.name+"age"+son.age);


```
var sTring = "Hello World";
sTring.length;//字符串长度，0开始
```
[String](http://www.w3school.com.cn/jsref/jsref_obj_string.asp "JavaScript String 对象")
```
var timeS = new Date();
//获取时间
document.write(timeS);
Tue Feb 23 2016 20:33:55 GMT+0800 (中国标准时间)

//获取年份
document.write(timeS.getFullYear());
```


```
Math

var pi_value=Math.PI;
var sqrt_value=Math.sqrt(15);

Math.max(x,y);
//返回 x 和 y 中的最高值。

```
[Date](http://www.w3school.com.cn/jsref/jsref_obj_date.asp "JavaScript Date 对象")


## 面向对象

```
//父类
function People(){
    
}
People.prototype.say = function(){
    alert("Hello");
}
function Student(){
    
}
Student.prototype = new People();

var s = new Student();
s.say();
```

```
//父类
function People(){
    
}
People.prototype.say = function(){
    alert("Hello");
}
function Student(){
    
}
Student.prototype = new People();
//复写方法
Student.prototype.say = function(){
    alert("Hellos");
}
var s = new Student();
s.say();
```
```
//父类
function People(){
    
}
People.prototype.say = function(){
    alert("Hello");
}
function Student(){
    
}
Student.prototype = new People();
//调用父类
var PoSsay = Student.prototype.say;
//复写方法
Student.prototype.say = function(){
    PoSsay.call(this);
    alert("Hellos");
}
var s = new Student();
s.say();
```

```
//父类
function People(name){
    this._name = name;
}
People.prototype.say = function(){
    alert("Hello"+this._name);
}
function Student(name){
    this._name = name;
}
Student.prototype = new People();
//调用父类
var PoSsay = Student.prototype.say;
//复写方法
Student.prototype.say = function(){
    PoSsay.call(this);
    alert("Hellos"+this._name);
}
var s = new Student("luuman");
s.say();
```

封装

```
(function(){
    var n = "SPFK";
    //父类
    function People(name){
        this._name = name;
    }
    People.prototype.say = function(){
        alert("Hello"+this._name+n);
    }
    //公开借口
    window.People = People;
}());
(function(){
    function Student(name){
        this._name = name;
    }
    Student.prototype = new People();
    //调用父类
    var PoSsay = Student.prototype.say;
    //复写方法
    Student.prototype.say = function(){
        PoSsay.call(this);
        alert("Hellos"+this._name);
    }
    }());
var s = new Student("luuman");
s.say();
```

```
function Person(){
    var _this = {};
    _this.sayHello = function(){
    alert("Hello");
    }
    return _this;
}

function Teacher(){
    var _this = Person();
    return _this;
}
var t = Teacher();
t.sayHello();
```


function A(){
    age:"12";
}
A.prototype={
    name: "luuman",
}
var B = new A();
alert(B.name);
alert(B.hasOwnProperty("name"));
alert(B.hasOwnProperty("age"));




























