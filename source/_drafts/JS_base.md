## 对象
ECMAScript 中的对象其实就是一组数据和功能的集合

创建Object 实例
```
1. 使用new 操作符后跟Object 构造函数
var person = new Object();如果不给构造函数传递参数，则可以省略后面的那一对圆括号。
2. 使用对象字面量表示法
var person = {};//与new Object()相同
var people = {name:"iwen",age:"30"};

一般来说，访问对象属性时使用的都是点表示法，这也是很多面向对象语言中通用的语法。不过，
在JavaScript 也可以使用方括号表示法来访问对象的属性。在使用方括号语法时，应该将要访问的属性
以字符串的形式放在方括号中，如下面的例子所示。
alert(people["name"]); //"iwen"
alert(people.name); //"iwen"
```
```
<script type="text/javascript">
    var person = new Object();
    person.name = 'Nicholas';
    person.age = 29;
    person.job = 'software Engineer';
    person.sayName = function(){alert(this.name);};

    var person = {
        name: 'Nicholas',
        age: 29,
        job: 'software Engineer',
        sayName: function(){
            alert(this.name);
        }
    };
</script>
```


Object 类型所具有的任何属性和方法，也同样存在于更具体的对象中。

```
constructor：保存着用于创建当前对象的函数。对于前面的例子而言，构造函数（constructor）就是Object()。
    <script type="text/javascript">
        var test = new Array();
        if(test.constructor == Array){document.write('This is an Array');}
        if(test.constructor == Boolean){document.write('This is an Boolean');}
    </script>
    <script type="text/javascript">
        function employee(name,job,born){
            this.name = name;
            this.job = job;
            this.born = born;
        }
        var bill = new employee('Bill Gates','Engineer',1895);
        document.write(bill.constructor);
    </script>

hasOwnProperty(propertyName)：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。
其中，作为参数的属性名（propertyName）必须以字符串形式指定（例如：o.hasOwnProperty("name")）。

isPrototypeOf(object)：用于检查传入的对象是否是传入对象的原型（第5 章将讨论原型）。

propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够使用for-in 语句
（本章后面将会讨论）来枚举。与hasOwnProperty()方法一样，作为参数的属性名必须以字符串形式指定。

toLocaleString()：返回对象的字符串表示，该字符串与执行环境的地区对应。

toString()：返回对象的字符串表示。

valueOf()：返回对象的字符串、数值或布尔值表示。通常与toString()方法的返回值相同。
```

```
<script type="text/javascript">
    function displayInfo(args){
        var output = '';
        if(typeof args.name == 'string'){
            output += 'Name: ' + args.name + '\n';
        }
        if(typeof args.age == 'number'){
            output += 'Age: ' + args.age + '\n';
        }
        alert(output);
    }
    displayInfo({name:'Nicholas',age:29});
    displayInfo({name:'Greg'});
</script>

```

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
## This
```
<script type="text/javascript">
    var people ={};
    people.show = function(){console.log(this)};//people
    people.onclick = function(){console.log(this)};//people

    function show(){console.log(this)}//window
    window.show = function(){console.log(this)}//window
    people.show();//people
    show();//window
</script>
```
Date日期 Array数组 RegExp正则 Object空白对象

## 面向对象
OOP面向对象编程（object-oriented programming）
ECMA-262 把对象定义为：“无序属性的集合，其属性可以包含基本值、对象或者函数。对象的每个属性或方法都有一个名字，而每个名字都映射到一个值（数据或函数）。
每个对象都是基于一个引用类型创建的，这个引用类型可以是第5 章讨论的原生类型，也可以是开发人员定义的类型。

封装：

继承：

多态：

function vs new:
```
<script type="text/javascript">
    function hide(name,age){
        var obj = new Object();
        obj.name = name;
        obj.age = age;
        obj.show = function(){console.log(this.name)};
        obj.hide = function(){console.log(this.age)};
        return obj;
    }
    var a = new hide('Nicholas','15');
    console.log(a.name);
    console.log(a.show());

    function show(){
        //var this = new Object();
        this.name = 'Nicholas';
        //return this;
    }
    var a = new show();
    console.log(a.name);
</script>
```
原型：
```
<script type="text/javascript">
    var arr = new Array(12,55);
    var arrs = new Array(12,55);
    arr.sum = function(){
        var result = 0;
        for(var i=0;i<this.length;i++){
            result += this[i];
        }
        return result;
    };
    alert(arr.sum());//67
    alert(arrs.sum());//bug no sum

    //原型
    var arr = new Array(12,55);
    var arrs = new Array(12,55);
    Array.prototype.sum = function(){
        var result = 0;
        for(var i=0;i<this.length;i++){
            result += this[i];
        }
        return result;
    };
    alert(arr.sum());//67
    alert(arrs.sum());//67
</script>
```

```
<script type="text/javascript">
    //父类
    function people(){}
    people.prototype.say = function(){
        alert('Hello');
    }
    function student(){}
    student.prototype = new people();
    var s = new student();
    s.say();
</script>
```

```
<script type="text/javascript">
    //父类
    function people(){}
    people.prototype.say = function(){
        alert('Hello');
    }
    function student(){}
    student.prototype = new people();
    
    var posSay = student.prototype.say;
    student.prototype.say = function(){
        posSay.call(this);
        alert('Hello');
    }
    var s = new student();
    s.say();
</script>
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
```



## 严格模式详解
[Javascript 严格模式详解](http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html "更新Pull")







xmlDoc = loadXMLDoc('books_ns.xml');
x = xmlDoc.getElementsByTagName('title')[0];
ns = 'http://wwww.w3school.com.cn/children/';
document.write(x.getAttributeNS(ns,'lang'));





## 元素属性操作HTML DOM

### getAttribute（）查看属性名的属性值

```
this.getAttribute('data-move');
document.getElementsByTagName("a")[0].getAttribute('data-move');
```

### setAttribute（）设置属性名的属性值

```
this.setAttribute("data-num",i);
document.getElementsByTagName("a")[0].setAttribute("data-num",i);
```

#### Javascript兼容性之——getAttribute(),setAttribute()（获取设置属性）

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">  
<html xmlns="http://www.w3.org/1999/xhtml">  
<head>  
<title>kingwell</title>  
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />  
<body>  
  
<div id="idHeader" class="class-header" title="kingwell" status="1"></div>  
<label id="forUserName" for="userName" title="kingwell" status="1"></label>  
  
</body>  
</html>  

var el = document.getElementById("idHeader");  
alert(el.getAttribute("id"));  
alert(el.id);  
IE Firfox->idHeader  
  
alert(el.getAttribute("class"));  
//IE6,IE7 -> null IE8,IE9,Firefox ->class-header  
  
alert(el.class);  
//IE6,IE7,IE8->报错 IE9,Firefox->undefined  
alert(el.getAttribute("className"));  
//IE6,IE7->class-header ; IE8,IE9,Firefox -> undefined  
  
alert(el.className);  
//All -> class-header  
  
  
var elfor = document.getElementById("forUserName");  
alert(elfor.getAttribute("for"));  
//IE6,IE7->undefined IE8,9,Firefox->forUseName  
  
alert(elfor.for )  
//IE6,IE7报错,其它为undefined  
alert(elfor.title)  
//全部输出kingwell  
alert(elfor.status);  
//IE6-8 -> 1 IE9,Firefox->undefined  
  
alert(elfor.getAttribute("status"))  
//全部输出 1  

总结：
    1:常规属性建议使用 node.XXXX。
    2:自定义属性建议使用node.getAttribute("XXXX")。
    3:当获取的目标是JS里的关键字时建议使用node.getAttribute("XXX")，如label中的for。
    4:当获取的目标是保留字,如：class,请使用className代替。

```
### 属性的编辑方法

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





## 面向对象



## 数据处理

### Math

#### 使用math随机计算数值：
```
"Y".replace(/Y/gi, Math.ceil(Math.random() * backgroundnum));
```

```
Math

var pi_value=Math.PI;
var sqrt_value=Math.sqrt(15);

Math.max(x,y);
//返回 x 和 y 中的最高值。
```

[Date](http://www.w3school.com.cn/jsref/jsref_obj_date.asp "JavaScript Date 对象")



[原生JS写Ajax的请求函数](http://caibaojian.com/ajax-jsonp.html "")
ajax({
    url: '/api_v4/Label/get_scenic_by_label',
    type: 'POST',
    data: {
        lat: '39.3245345',
        lng:'116.3403167725',
        p:'1',
        label_id:'84',
    },
    dataType: 'json',
    success: function(response,xml){
        console.log(response);
    },
    fail: function(status){}
});
function ajax(options){
    options = options || {};
    options.type = (options.type || 'GET').toUpperCase();
    options.dataType = options.dataType || 'json';
    var params = formatParams(options.data);
    if(window.XMLHttpRequest){
        var xhr = new XMLHttpRequest();
    }else{
        var xhr = new ActiveXObject('Microsoft.XMLHTTP');
    }
    xhr.onreadystatechange = function (){
        if(xhr.readyState == 4){
            var status = xhr.status;
        if(status >= 200 && status < 300){
            options.success && options.success(xhr.responseText, xhr.responseXML);
        }else{
            options.fail && options.fail(status);
        }
        }
    }
    if (options.type == "GET") {
        xhr.open("GET", options.url + "?" + params, true);
        xhr.send(null);
    } else if (options.type == "POST") {
        xhr.open("POST", options.url, true);
        xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded"); xhr.send(params); 
    }
}
      function formatParams(data) { var arr = []; for (var name in data) { arr.push(encodeURIComponent(name) + "=" + encodeURIComponent(data[name])); } arr.push(("v=" + Math.random()).replace(".","")); return arr.join("&"); }
      