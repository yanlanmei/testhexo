title: Hexo插件安装
date: 2015-12-27 18:29:00
description: 
categories:
- 建站
tags:
- 博客
- 建站
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
# 安装分享按钮

```
去百度分享获取分享代码
配置

vim themes/light/layout/_partial/article.ejs
删除
<%-partial('post/share')%>
替换为刚刚获取的分享代码

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
```

# 安装百度统计

去百度统计获取统计代码

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

# 不蒜子
themes/你的主题/layout/_partial/footer.ejs

```
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