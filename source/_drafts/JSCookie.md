Cookie

同一个网站，只有一套Cookie
适浏览器而定：
Cookie的大小4kb-10kb，大小十分有限
网站不会超过50条
不用的Cookie要删除，条数有限

过期时间
用Firefox进行测试，Chrome、IE都会把本地Cookie干掉。

JS
//属性
document.cookie

编辑

//添加Cookie
document.cookie='user=bus';
document.cookie='pass=sbus';//不是赋值

过期时间
//
var oDate = new Date();
oDate.setDate(oDate.getDate()+14);

//传入名称、值、时间
function setCookie(name,value,iDay){
	var oDate = new Date();
	oDate.setDate(oDate.getDate()+iDay);//过期时间多少天

	document.cookie = name + '=' + value + ';expires=' + oDate;
}
setCookie('userName','Luumans',12);

//获取Cookie值
function getCookie(name){
	//字符串分割
	var aType = document.cookie.split('; ');
	
	for(var i=0;i<aType.length;i++){
		//字符串分割
		var aName = aType[i].split('=');
		//判断名称
		if(aName[0]==name){
			return aName[1];
		}
	}
	return '';//Null
}
alert(getCookie('name'));

//删除Cookie

function removeCookie(name){
	setCookie(name,1,-1);
}
removeCookie('name');



//实例登录

<form action="http://www.baidu.com">
	<input type="text" name="user" /><br />
	<input type="password" name="pass" /><br />
	<input type="submit" value="登录" />
</form>

<script type="text/javascript">
	window.onload = function(){
		var uForm = document.getElementById('from1');
		var oUser = document.getElementById('user')[0];

		uForm.onsubmit = function(){
			setCookie('user',oUser.value,14);
		};
		oUser.value = getCookie('user')
	}
	function setCookie(name,value,iDay){
		var oDate = new Date();
		oDate.setDate(oDate.getDate()+iDay);//过期时间多少天

		document.cookie = name + '=' + value + ';expires=' + oDate;
	}
</script>


淘宝、百度的Cookie病毒式使用：ACookie、

H5：存储localstrang

获取两个标签的共同的父标签
function getTag(A,B){
	var AID = document.getElementById('A').
}

计算字符串中出现最多的字符的个数
function getString(){
}