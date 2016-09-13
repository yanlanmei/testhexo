
```
```

```
//定义构造函数以初始化新的对象
function aPoint(x,y){
	this.x = x;
	//将函数参数存储为对象的属性
	this.y = y;
}
//通过对象属性添加方法
aPoint.prototype.r = function(){
	return Math.sqrt(this.x * this.x + this.y * this.y);
};
//使用new关键字和构造函数创建一个实例
var p = new aPoint(2,3);
//构造函数对象实例，都继承了方法 r();
p.r();
```

```
//封装函数
function ajax(url,fnSucc,fnFaild){
	if(window.XMLHttpRequest){
		var oAjax = new XMLHttpRequest();
	}else{
		var oAjax = new ActiveXObject("Microsoft.XMLHTTP");
	}

	oAjax.opan('GET','url?=t'+new Date().getTime(),true);

	oAjax.send();

	oAjax.onreadystatechange = function(){
		if(oAjax.readyState==4){
			if(oAjax.status==200){
				fnSucc(oAjax.responseText);
			}else{
				if(fnFaild){
					fnFaild(oAjax.status);
				}
			}
		}
	}
}

ajax('a.txt',function(str){
	alert(str);
})
```





//在document指定区域输出
function debug(msg){
	var log = document.getElementById("debuglog");

	if (!log){
		//创建一个新元素
		log = document.createElement("div");
		log.id = "debuglog";
		log.innerHTML = "<h1>Debug Log</h1>";
		//将其添加到文档末尾
		document.body.appendChild(log);
	}

	var pre = document.createElement("pre");
	//将文档包装在一个文本节点中
	var text = document.createTextNode(msg);
	pre.appendChild(text);
	log.appendChild(pre);
}
debug("nihao hailjdskf djfkdsl ");