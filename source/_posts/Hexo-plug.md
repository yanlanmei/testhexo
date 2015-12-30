title: Hexo插件安装
date: 2015-12-27 18:29:00
description: 
categories:
- Hexo
tags:
- Hexo
toc: true
author:
comments:
original:
permalink: 
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。
　　在此记录自己已理解并开始遵循的前端代码规范。What How Why
　　最近，使用Hexo遇到了很多问题，在设立进行整理。

<!-- more -->
## 同步instagram图片

### 新建页面

```
执行命令：
hexo new page "instagram"
```
### 修改文件

```
在目录yourBlog\source\instagram下，修改index.md内容为：

---
layout: post
slug: "instagram"
title: "相册"
noDate: "true"
---

<div class="instagram" data-client-id="a0d4bd    ab154b4c689aff70602cb34a2c" data-user-id="438522285">
    <a href="http://instagram.com/litten225" target="_blank" class="open-ins">图片来自instagram，正在加载中…</a>
</div>
<script src="/js/jquery.lazyload.js"></script>
<script src="/js/instagram.js"></script>
```
### 获取ID
data-client-id：
[注册新客户端](http://instagram.com/developer/clients/manage/)
获取CLIENT ID：a0d4bdab154b4c689aff70602cb34a2c
用client_id去换取token：
在浏览器中请求：

    https://instagram.com/oauth/authorize/?client_id={CLIENT_ID}&redirect_uri={REDIRECT_URI}&response_type=token
    https://instagram.com/oauth/authorize/?client_id=a0d4bdab154b4c689aff70602cb34a2c&redirect_uri=http://luuman.github.io/&response_type=token
    花括号里面的值，对应上一步最终得到的client_id和自己设定的redirect_uri。
    请求到的是一个授权页面，授权完毕后，则重定向到你的redirect_uri。
    注意看授权成功后的url，hash部分会附带给你的token。至此，token成功获取。

data-user-id：

需要到[lookup-user-id](http://jelled.com/instagram/lookup-user-id#)填写用户名并查找。

## 安装分享按钮

```
去百度分享获取分享代码
配置

vim themes/light/layout/_partial/article.ejs
删除
<%-partial('post/share')%>
替换为刚刚获取的分享代码

32px
<div class="bdsharebuttonbox"><a href="#" class="bds_more" data-cmd="more"></a><a href="#" class="bds_tsina" data-cmd="tsina" title="分享到新浪微博"></a><a href="#" class="bds_tieba" data-cmd="tieba" title="分享到百度贴吧"></a><a href="#" class="bds_qzone" data-cmd="qzone" title="分享到QQ空间"></a><a href="#" class="bds_youdao" data-cmd="youdao" title="分享到有道云笔记"></a><a href="#" class="bds_linkedin" data-cmd="linkedin" title="分享到linkedin"></a><a href="#" class="bds_fbook" data-cmd="fbook" title="分享到Facebook"></a><a href="#" class="bds_print" data-cmd="print" title="分享到打印"></a><a href="#" class="bds_copy" data-cmd="copy" title="分享到复制网址"></a></div>
<script>window._bd_share_config={"common":{"bdSnsKey":{},"bdText":"","bdMini":"2","bdMiniList":false,"bdPic":"","bdStyle":"2","bdSize":"32"},"share":{}};with(document)0[(getElementsByTagName('head')[0]||body).appendChild(createElement('script')).src='http://bdimg.share.baidu.com/static/api/js/share.js?v=89860593.js?cdnversion='+~(-new Date()/36e5)];</script>

    .bdshare-button-style2-32{
      width: 346px;
      margin: auto;
    }
    @media screen and (max-width:640px) {
      .bdshare-button-style2-32{
        width: 320px;
        margin: auto;
      }
    }

24px
<div class="bdsharebuttonbox"><a href="#" class="bds_more" data-cmd="more"></a><a href="#" class="bds_tsina" data-cmd="tsina" title="分享到新浪微博"></a><a href="#" class="bds_linkedin" data-cmd="linkedin" title="分享到linkedin"></a><a href="#" class="bds_print" data-cmd="print" title="分享到打印"></a><a href="#" class="bds_copy" data-cmd="copy" title="分享到复制网址"></a><a href="#" class="bds_tieba" data-cmd="tieba" title="分享到百度贴吧"></a><a href="#" class="bds_qzone" data-cmd="qzone" title="分享到QQ空间"></a><a href="#" class="bds_renren" data-cmd="renren" title="分享到人人网"></a></div>
<script>window._bd_share_config={"common":{"bdSnsKey":{},"bdText":"","bdMini":"2","bdMiniList":false,"bdPic":"","bdStyle":"2","bdSize":"24"},"share":{}};with(document)0[(getElementsByTagName('head')[0]||body).appendChild(createElement('script')).src='http://bdimg.share.baidu.com/static/api/js/share.js?v=89860593.js?cdnversion='+~(-new Date()/36e5)];</script>

D:\Hexo\Hexo\themes\spfk\source\css\_partial\article.styl

.bdshare-button-style2-24{
  width: 248px;
  margin: auto;
}
```

## 安装百度统计

### 去百度统计获取统计代码

```
vim themes/light/layout/_partial/baidu_analytics.ejs

<% if (theme.baidu_analytics){ %>
<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "//hm.baidu.com/hm.js?819b1c6493df653afb8c784db6";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>

<% } %>

vim hexo/themes/light/_config.yml

baidu_analytics: true

vim hexo/themes/light/layout/_partial/head.ejs
在/head前添加

<%- partial('baidu_analytics') %>
</head>
```

## 不蒜子
### 代码修改

```
themes/你的主题/layout/_partial/footer.ejs

<footer id="footer">
    <div class="outer">
        <div id="footer-info">
            <div class="footer-left">
                &copy; <%= date(new Date(), 'YYYY') %> <%= config.author || config.title %>
            </div>
            <div class="footer-right">
                <a href="http://hexo.io/" target="_blank">Hexo</a>  Theme <a href="https://github.com/luuman/hexo-theme-spfk" target="_blank">spfk</a> by luuman
            </div>
        </div>
        <div class="visit">
            <span id="busuanzi_container_site_pv" style='display:none'>
                <span id="site-visit" >本站到访数: 
                    <span id="busuanzi_value_site_uv"></span>
                </span>
            </span>
            <span id="busuanzi_container_page_pv" style='display:none'>
                <span id="page-visit">, 本页阅读量: 
                    <span id="busuanzi_value_page_pv"></span>
                </span>
            </span>
        </div>
    </div><script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js">
</script>
</footer>
```

### 样式美化

移动端出现上移themes\spfk\source\css\_partial\mobile.styl
```
#footer {
    bottom: 10px;
    .footer-left{
        float: initial;
        margin-bottom: 10px;
    }
    .footer-right{
        float: initial;
        margin-bottom: 10px;
    }
}
#container .visit {
    margin-top: 1em;
}
```


## 添加版权声明

### 添加代码

```
\layout\_partial\post\nav.ejs

<% if (post.original != false && !is_page()){ %>
    <div class="copyright">
        <p><span>本文标题:</span><a href="<%- url_for(post.path) %>"><%= post.title %></a></p>
        <p><span>文章作者:</span><a href="/" title="请访问 <%=theme.author%> 博客"><%=theme.author%></a></p>
        <!-- <p><span>发布时间:</span><%= post.date.format("YYYY年MM月DD日 - HH时mm分") %></p> -->
        <!-- <p><span>最后更新:</span><%= post.updated.format("YYYY年MM月DD日 - HH时mm分") %></p> -->
        <p>
            <span>原始链接:</span><a class="post-url" href="<%- url_for(post.path) %>" title="<%= post.title %>"><%= post.permalink %></a>
            <span class="copy-path" data-clipboard-text="原文: <%= post.permalink %>　　作者: <%=theme.author%>" title="点击复制文章链接"><i class="fa fa-clipboard"></i></span>
            <script src="/js/clipboard.min.js"></script>
            <script> var clipboard = new Clipboard('.copy-path'); </script>
        </p>
        <p>
            <span>许可协议:</span><i class="fa fa-creative-commons"></i> <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/3.0/cn/" title="中国大陆 (CC BY-NC-SA 3.0 CN)">"署名-非商用-相同方式共享 3.0"</a> 转载请保留原文链接及作者。
        </p>
    </div>
<% } %>

<% if (post.prev || post.next){ %>
<nav id="article-nav">
  <% if (post.prev){ %>
    <a href="<%- url_for(post.prev.path) %>" id="article-nav-newer" class="article-nav-link-wrap">
      <strong class="article-nav-caption"><</strong>
      <div class="article-nav-title">
        <% if (post.prev.title){ %>
          <%= post.prev.title %>
        <% } else { %>
          (no title)
        <% } %>
      </div>
    </a>
  <% } %>
  <% if (post.next){ %>
    <a href="<%- url_for(post.next.path) %>" id="article-nav-older" class="article-nav-link-wrap">
      <div class="article-nav-title"><%= post.next.title %></div>
      <strong class="article-nav-caption">></strong>
    </a>
  <% } %>
</nav>
<% } %>
```

### 修改样式