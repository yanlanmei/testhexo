title: Hexo的使用介绍
date: 2015-12-25 18:29:00
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
permalink: web-style-guide
---

　　**自用笔记：**本文属于自用笔记，不做详解，仅供参考。
　　在此记录自己已理解并开始遵循的前端代码规范。What How Why
　　最近，使用Hexo遇到了很多问题，在设立进行整理。

<!-- more -->
>写文章

```
    $ hexo n #写文章

    文章开头语法：
        title: name #文章标题
        date: 2015-12-25 18:29:00  #写作时间
        description: #文章描述
        categories: #文章分类
        - 建站
        tags: #文章标签
        - 博客
        - 建站
        - Hexo
        toc: #生成目录
        author:
        comments:
        original:
        permalink: web-style-guide
        ---

        以上是摘要
        <!--more-->

        以下是余下全文
```
>写多种文章

```
    $ hexo new [layout] "postName" #新建文章
    [layout]：其中layout是可选参数，默认值为post。有哪些layout呢，请到 scaffolds 目录下查看，这些文件名称就是layout名称。当然你可以添加自己的layout，方法就是添加一个文件即可，同时你也可以编辑现有的layout，比如post的layout默认是 hexo\scaffolds\post.md
```
>写页面（404）

```
    $ hexo new page "404"

    UUhike@UUhike-pc MINGW64 /d/Hexo/Hexo (master)
    $ hexo new page "404"
    INFO  Created: D:\Hexo\Hexo\source\404\index-1.md
```
>配置配置“多说”留言

```
    ├── spfk
        ├── _config.yml #主题配置文件
    #是否开启多说评论，填写你在多说申请的项目名称 duoshuo: duoshuo-key（http://duoshuo-key.duoshuo.com/）
    #若使用disqus，请在博客config文件中填写disqus_shortname，并关闭多说评论
    duoshuo: true


复制到 themes\landscape\layout\_partial\article.ejs把

<% if (!index && post.comments && config.disqus_shortname){ %>
<section id="comments">
<div id="disqus_thread">
<noscript>Please enable JavaScript to view the <a href="//disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
</div>
</section>
<% } %>

改为

<% if (!index && post.comments && config.disqus_shortname){ %>
<section id="comments">
<!-- 多说评论框 start -->
<div class="ds-thread" data-thread-key="<%= post.layout %>-<%= post.slug %>" data-title="<%= post.title %>" data-url="<%= page.permalink %>"></div>
<!-- 多说评论框 end -->
<!-- 多说公共JS代码 start (一个网页只需插入一次) -->
<script type="text/javascript">
var duoshuoQuery = {short_name:'<%= config.disqus_shortname %>'};
  (function() {
    var ds = document.createElement('script');
    ds.type = 'text/javascript';ds.async = true;
    ds.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') + '//static.duoshuo.com/embed.js';
    ds.charset = 'UTF-8';
    (document.getElementsByTagName('head')[0] 
     || document.getElementsByTagName('body')[0]).appendChild(ds);
  })();
  </script>
<!-- 多说公共JS代码 end -->
</section>
<% } %>
```

>发布博客内容
实现发布，前提是配置好GitHub文件内容。

```
    $ hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）Hexo 会监视文件变动并自动更新，您无须重启服务器。

    $ hexo g #生成
    $ hexo generate #生成静态页面至public目录（最终上传这个文件到GitHub）

    $ hexo d == hexo deploy#部署
    $ hexo d #部署 # 可与hexo g合并为 hexo d -g

    $ hexo deploy -g
    $ hexo server -g # 生成默认文件群再执行,开启本地静态html服务器
```

>主题的更改

```
    建立了Hexo文件，复制我的主题了到themes文件夹中
    yilia
    $ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
    modernist
    $ git clone https://github.com/heroicyang/hexo-theme-modernist.git themes/modernist
    jacman
    $ git clone https://github.com/cnfeat/cnfeat.git themes/jacman
```


>文章图片路径
Hexo如何方式图片，图片应该放置到哪里，不会应为上传而覆盖掉。然后把文章里的index.md删除，将文件存放在resource文件夹中间。

```
    发布页面
    $ hexo new page "name" # 新建一个页面，页面名称name

    UUhike@UUhike-pc MINGW64 /d/Hexo/Hexo (master)
    $ hexo new page "resoures"
    INFO  Created: D:\Hexo\Hexo\source\resoures\index.md
```

>RSS不显示

```
    安装RSS插件

    npm install hexo-generator-feed --save

    开启RSS功能

    编辑hexo/_config.yml，添加如下代码：

    rss: /atom.xml #rss地址  默认即可
```
>创建instagram

```
$ hexo new page "instagram"

在目录yourBlog\source\instagram下，修改index.md内容为：

    layout: post
    slug: "instagram"
    title: "相册"
    noDate: "true"
    ---

<div class="instagram" data-client-id="956dd096b6e5496aba6662165b9b8443" data-user-id="438522285">
    <a href="http://instagram.com/litten225" target="_blank" class="open-ins">图片来自instagram，正在加载中…</a>
</div>
<script src="/js/jquery.lazyload.js"></script>
<script src="/js/instagram.js"></script>


    注意其中的data-client-id属性，是你instagram上的client-id(不是用户id)。
    具体可到instagram-manage网站上去获得。
    data-user-id属性，需要到lookup-user-id查找并填写。
```