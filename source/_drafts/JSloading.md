页面Loading加载原理


原理：
通过加载完成，隐藏loading动画，为了防止有部分


通常情况下：
会使用onload，判断页面是否加载完成。window.onload = function(){}

查看乐视品牌H5页面，分析出事先定义loadtime的最小时间3s。

方法：
使用opticy: 0;来隐藏loading的页面，使用display: none;

//关闭Loading
var loadTime = 3000 + startTime - (new Date()).getTime();
if(loadTime<=0){ loadTime = 500; };
  if($('#spinner').length == 0){
    loadTime = 500;
  }
  setTimeout(function(){
    $('#spinner').css('display', 'none');
    firstPage.css('display','none');

    if ($('.barrage-container').length) {
        $.fn.danmu ? loadDanmu()
        : asyLoadScript(cdnUrl+'/static/pc/invitation/js/danmu.js', 'js', loadDanmu);
    } else {
        firstPageStart();
    }
    if ($('.form-imgupload').length){
        asyLoadScript(cdnUrl+'/static/invitation/js/imgUpload.js', 'js');
    }
    loadTime = startTime = null;
  },loadTime);


function d() {
    j++, 1 === j && setTimeout(function () {
        $("html").removeClass("lock"), $("#loading-container").addClass("hide"), setTimeout(function () {
            $("#loading-container").hide()
        }, 500)
    }, 600)
}




方法二：JQuery实现页面加载完成，隐藏loading元素




<link rel="stylesheet" href="/css/loading-style.css">
<div id="loader-wrapper">
	<div id="loader"></div>
</div>
<!-- loading -->
<script>window.jQuery || document.write('<script src="/js/jquery-1.9.1.min.js"><\/script>')</script>
<script type="text/javascript">
    $(window).load(function() {
        $('#loader').fadeOut();
		$('#loader-wrapper').delay(50).fadeOut('slow');
        $('body').delay(50).css({'overflow-y':'visible'});
    })
</script>



<script type="text/javascript">
	(function () {
	    var ie = !!(window.attachEvent && !window.opera);
	    var wk = /webkit\/(\d+)/i.test(navigator.userAgent) && (RegExp.$1 < 525);
	    var fn = [];
	    var run = function () { for (var i = 0; i < fn.length; i++) fn[i](); };
	    var d = document;
	    d.ready = function (f) {
	        if (!ie && !wk && d.addEventListener)
	            return d.addEventListener('DOMContentLoaded', f, false);
	        if (fn.push(f) > 1) return;
	        if (ie)
	            (function () {
	                try { d.documentElement.doScroll('left'); run(); }
	                catch (err) { setTimeout(arguments.callee, 0); }
	            })();
	        else if (wk)
	            var t = setInterval(function () {
	                if (/^(loaded|complete)$/.test(d.readyState))
	                    clearInterval(t), run();
	            }, 0);
	    };
	})();

	document.ready(function () {
	    progress();
	});
</script>




loading动画：

## eyepetizer

[让眼睛不断旋转](file:///G:/Web/H5/eyepetizer/index.html "")


文档加载：
window.onload = function(){}

	window.onload只能执行最后一个，必须等到页面内包括图片的所有元素加载完毕后才能执行。


$(window).load(function(){})

$(document).ready(function(){})
$(fucntion(){})
是DOM结构绘制完毕后就执行，不必等到加载完毕。
可以在一个页面中重复出现，而不会冲突。







1.执行时间
    window.onload必须等到页面内包括图片的所有元素加载完毕后才能执行。
    $(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕。 
2.编写个数不同
    window.onload不能同时编写多个，如果有多个window.onload方法，只会执行一个
    $(document).ready()可以同时编写多个，并且都可以得到执行
3.简化写法
    window.onload没有简化写法
    $(document).ready(function(){})可以简写成$(function(){});

在我以前的开发中，一般用到javascript，我都是采用jquery的模式，也就是大多数时候，第一行写的是：


复制代码 代码如下:
$(document).ready(function(){
…
});

这个时候，不一定要等所有的js和图片加载完毕，就可以执行一些方法，不过有些时候，必须要等所有的

元素都加载完毕，才可以执行一些方法的时候，比如说，部分图片或者什么其他方面还没有加载好，这个时候，点击某些按钮，会导致出现意外的情况，这个时候，就

需要用到:


复制代码 代码如下:
$(window).load(function() {
…

});


总结对比：

```
```
<script type="text/javascript">
// Not Ready
(function(){
	console.log('Not_Ready');
})();
	
// Dom_Ready
$(document).ready(function(){
	console.log('Dom_Ready');
});

// Dom_Ready
$(function(){
	console.log('Dom_Ready');
});

// All_Ready
$(window).load(function(){
	console.log('All_Ready');
});

window.onload = function(){}
</script>