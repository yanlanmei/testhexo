/* 
* @Author: luuman
* @Last Modified by:   luuman
* @Date:   2016-06-12 13:13:56
* @Last Modified time: 2016-04-07 14:29:18
* @Function: New App Interface arrangement
*/

// 七牛图片数据：http://pic.tipuyou.cn/act/act6614/640.webp%20%287%29.gif

/**
 * App 旅图跳转
1. 评论列表
var dic = {'type': '1', 'id': '', 'extra': ''};
2. 点赞列表
var dic = {'type': '2', 'id': '', 'extra': ''};
3. 城市详情页
var dic = {'type': '3', 'id': '', 'extra': ''};
4. 景区详情页
var dic = {'type': '4', 'id': '', 'extra': ''};
5. 首页
var dic = {'type': '5', 'id': '', 'extra': ''};
6. 景点详情页
var dic = {'type': '6', 'id': '景点id', 'extra': '景区id'};
7. URL
var dic = {'type': '7', 'id': '', 'extra': 'URL'};
8. 邀请列表页
var dic = {'type': '8', 'id': '', 'extra': ''};
9. 加入的群组页
var dic = {'type': '9', 'id': '', 'extra': ''};
10. 退出的群组页
var dic = {'type': '10', 'id': '', 'extra': ''};
11. 发布旅图页
var dic = {'type': '11', 'id': '2', 'extra': '#用美食，祭身材#'};
12. 用户信息
var dic = {'type': '12', 'id': '', 'extra': ''};
13. 旅图列表页
var dic = {'type': '13', 'id': '', 'extra': ''};
14. 旅图详情页
var dic = {'type': '14', 'id': '', 'extra': ''};
15. 话题旅图列表页
var dic = {'type': '15', 'id': '', 'extra': ''};
16. 主题详情页
var dic = {'type': '16', 'id': '', 'extra': ''};
17. 私信聊天页
var dic = {'type': '17', 'id': '', 'extra': ''};
18. 地图中的位置共享聊天页
var dic = {'type': '18', 'id': '', 'extra': ''};
19. 特定商品详情
var dic = {'type': '19', 'id': '', 'extra': ''};
20. 商品分类的商品列表页面
var dic = {'type': '20', 'id': '', 'extra': ''};
21. 电商活动页面
var dic = {'type': '21', 'id': '', 'extra': ''};
22. 商家店铺页面
var dic = {'type': '22', 'id': '', 'extra': ''};
23. 特定订单详情
var dic = {'type': '23', 'id': '', 'extra': ''};

24. 地图
var dic = {'type': '24', 'id': '景区ID', 'extra': '可选景点ID'};
*/

function AppJump(){
    var dic = {'type': '11', 'id': '2', 'extra': '#用美食，祭身材#'};
    UserModel.jsCallNativeJumpWithDic(dic);
}
function jump(dic){
    var ua = navigator.userAgent;
    var isAndroid = ua.indexOf('Android') > -1 || ua.indexOf('Adr') > -1;
    var isiOS = !!ua.match(/\(i[^;]+;(U;)? CPU. + Mac OS X/);
    try{
        if(isAndroid){
            var dics = JSON.stringify(dic);
            UserModel.jsCallNativeJumpWithDic(dics);
        }else if(isiOS){
            UserModel.jsCallNativeJumpWithDic(dic);
        }
    }catch(err){
        try{
            UserModel.scenicInfo('6187');
        }catch(err){
            window.location.href = 'http://a.app.qq.com/o/simple.jsp?pkgname=com.jingqubao.tips';
        }
    }
}
/**
 * App
 1.获取版本号 2.是否登录 3.纯文本提示 （string字符串）
	var dic = {'type': '1', 'text': ''};
	var dic = {'type': '2', 'text': ''};
	var dic = {'type': '3', 'text': 'bcvxdgdxg'};
*/
function appV(){
    var dic = {'type': '1'};
    UserModel.jsCallNativeAlterWith(dic);
}
function appLogin(){
    var dic = {'type': '2'};
    UserModel.jsCallNativeAlterWith(dic);
}
function appTitle(){
    var dic = {'type': '3', 'text': '纯文本提示'};
    UserModel.jsCallNativeAlterWith(dic);
}

/**
 * 判断是否在 App中浏览
 */
var appV = 'null';
try{
    appV = UserModel.getAppVersion;
}catch(err){
    AppDownload();
    alert('liu');
}
if(!appV == 'null'){
    alert('app');
}


//在微信中隐藏
var ua = navigator.userAgent.toLowerCase();
if(ua.match(/MicroMessenger/i) == "micromessenger"){  
    $(".share").css("display","none");
    AppWeiShare();
}

// 分享信息提取
function AppWeiShare(){
    // 分享定制
    var oUrl = '';
    var oTitle = '';
    var oDesc = '';
    var oImgUrl = '';
    if(typeof(UserModel) !== "undefined"){
        UserModel.shareContentIconUrlTargetUrl(oTitle,oDesc,oImgUrl,oUrl);  //分享接口
    }else{
        WeiShare(oUrl,oTitle,oDesc,oImgUrl);
    }
}


// 分享定制
var oUrl = '';
var oTitle = '';
var oDesc = '';
var oImgUrl = '';

/**
 * App 分享接口
 * 接口 - 
 */
function AppShareV1(oUrl,oTitle,oDesc,oImgUrl){
    UserModel.shareContentIconUrlTargetUrl(oTitle,oDesc,oImgUrl,oUrl);  //分享接口
}
function AppShareV2(oUrl,oTitle,oDesc,oImgUrl){
    var dic = {'title': oTitle,'text': oDesc,'url': oUrl,'img': oImgUrl,};
    UserModel.jsCallNativeShareWithDic(dic);
}

/**
 * 微信分享定制接口
 */
// <script type="text/javascript" src="http://res.wx.qq.com/open/js/jweixin-1.0.0.js"></script>
wx.config({
    debug: false,
    appId: 'wxdcb447934ddf8be6',
    timestamp: '<?php echo $timestamp ?>',
    nonceStr: '<?php echo $noncestr; ?>',
    signature: '<?php echo $sign ?>',
    jsApiList: [
        'checkJsApi',
        'onMenuShareTimeline',
        'onMenuShareAppMessage',
        'onMenuShareQQ',
        'onMenuShareWeibo']
});
wx.ready(function(){

    // 设置"发送给朋友圈"参数
    wx.onMenuShareTimeline({
      title: oTitle,          // 分享标题
      link: oUrl,             // 分享链接
      imgUrl: oImgUrl,        // 分享图标
      success: function(res) {}, // 用户确认分享后执行的回调函数
      cancel: function() {} // 用户取消分享后执行的回调函数
    });
    // 设置"发送给朋友"参数
    wx.onMenuShareAppMessage({
        title: oTitle,          // 分享标题
        desc: oDesc, // 分享描述
        link: oUrl,             // 分享链接
        imgUrl: oImgUrl,        // 分享图标
        success: function() {}, // 用户确认分享后执行的回调函数
        cancel: function() {} // 用户取消分享后执行的回调函数
    });
    // 设置"发送给QQ"参数
    wx.onMenuShareQQ({
        title: oTitle,          // 分享标题
        link: oUrl,             // 分享链接
        imgUrl: oImgUrl,        // 分享图标
        success: function() {}, // 用户确认分享后执行的回调函数
        cancel: function() {} // 用户取消分享后执行的回调函数
    });
});

/**
 * 页面统计数据
 */

function sum(number){
    $.ajax({
        type: 'GET',
        url: 'http://v2.jingqubao.com/w3g/Statistic/record',
        data: {
            url: number,
            status:'1',
            type:'act_',
        },
        dataType: 'json',
        success: function(){
        },
        error: function(){
        },
    });
}

/**
 * 页面跳转下载页面
 */
function AppDown(){
    window.location.href= 'http://a.app.qq.com/o/simple.jsp?pkgname=com.jingqubao.tips';
}

/**
 * 打开景区宝App
 * 接口 - tipsTravel;
 */
function openApp(){
    var u = navigator.userAgent;
    var URLs = "";
    var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1; //android终端
    var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
    if(isAndroid){
        URLs = "tipstravelapp://openapp";
    }else if(isiOS){
        URLs = "tipsTravelApp://openapp";
    }
    location.href = URLs;
    var n = window.navigator.userAgent, e = "";
    e = /iphone/i.test(n) && /micromessenger/i.test(n)?"http://a.app.qq.com/o/simple.jsp?pkgname=com.jingqubao.tips":"http://jingqubao.com" + location.search,document.getElementById("go").setAttribute("href",e)
}
function openApp(){
    var u = navigator.userAgent;
    var URLs = "";
    var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1; //android终端
    var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
    if(isAndroid){
        URLs = "tipstravelapp://openapp";
    }else if(isiOS){
        URLs = "tipsTravelApp://openapp";
    }
    window.location = URLs;
        setTimeout(
            function(){
            window.location="http://a.app.qq.com/o/simple.jsp?pkgname=com.jingqubao.tips";
        }, 5000);
}


/**
 * 微信分享弹窗：
 */
function shareWeixin(){
    var oDiv = document.createElement("div");
    oDiv.id = "share_weixin";
    var data_img = "data:image/png;base64,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";
    var sdiv = "position:fixed;left:0;top:0;width:100%;height:100%;background:rgba(0,0,0,0.6);z-index:9999;";
    var simg = "width:200px;float:right;padding:6px;";

    var oTexts = '<div style="'+ sdiv +'"><img style="'+ simg +'" src="' + data_img + '"></div>';
    oDiv.innerHTML = oTexts;
    document.body.appendChild(oDiv);
    oDiv.onclick = function(){
        document.body.removeChild(oDiv);
    }
}

/**
 * App app下载
 * 接口 - (void)share:(NSString *)title content:(NSString *)content iconUrl:(NSString *)iconUrl targetUrl:(NSString *)targetUrl;//分享
 */
function AppDownload(){
    var sText = document.createElement('style');
    sText.type = 'text/css';
    sText.setAttribute('data-name','tip-loading');
    sText.innerHTML = '.appD{display:none;position:fixed;top:0;left:0;width:100%;height:60px;background:#747E89;z-index:999}'
        + '.appD .appLogo{width:40px;height:40px;padding:10px 0;float:left}'
        + '.appD .appOff{float:left;width:20px;height:20px;margin:20px 10px;background:url(http://v2.jingqubao.com/apps/w3g/_static/img/new_vote/buttom_off.png) no-repeat;background-size:20px 20px}'
        + '.appD .appDown{position:absolute;color:#FFF;background:#FFD700;width:74px;height:24px;margin:16px 5px;font-size:12px;line-height:24px;text-align:center;display:inline-block;border:2px solid #FFF;border-radius:60px;right:0;top:0}'
        + '.appD .appText{color:#FFF;padding:9px 0;margin-left:90px;margin-right:88px;font-size:12px}'
        + '.appD .appText .appTitle{font-size:16px}'
        + '.appD .appText .appT{text-overflow:ellipsis;white-space:nowrap;overflow:hidden}';
    document.getElementsByTagName('head')[0].appendChild(sText);

    var oDiv = document.createElement('div');
    oDiv.id = 'app_download';
    var textHtml = '<div class="appD"><a class="appOff" href="javascript:;"></a><img class="appLogo" src="http://v2.jingqubao.com/apps/w3g/_static/img/new_vote/logo.png"><div class="appText"><p class="appTitle">下载提谱旅行APP</p><p class="appT">免费贴身导游，海量游玩贴士玩转全国景区。</p></div><a class="appDown" href="javascript:;">马上下载</a></div>';
    oDiv.innerHTML = textHtml;
    document.body.appendChild(oDiv);
}

// app下载
var ua = navigator.userAgent.toLowerCase();
if(ua.match(/MicroMessenger/i) == "micromessenger") {
    $(".appD").css("display","block");
}
$(".appOff").click(function(){
    $(".appD").css("display","none");
})
$(".appDown").click(function(){
    if(typeof(UserModel) !== "undefined"){
        $(".appD").css("display","none");
    }
    window.location = "http://a.app.qq.com/o/simple.jsp?pkgname=com.jingqubao.tips";
})

/**
 * App 分享
 */
function AppTopShare(){
    var oDiv = document.createElement('div');
    oDiv.id = 'app_top_share';
    var textHtml = '<div style="position: fixed;right: 10px;top: 10px;width: 40px;height: 40px;border-radius: 30px;background: url(http://v2test.jingqubao.com/apps/w3g/_static/img/vote/share.png) rgba(0, 0, 0, 0.79) no-repeat center;background-size: 21px;z-index: 999;"></div>';
    oDiv.innerHTML = textHtml;
    document.body.appendChild(oDiv);
}
