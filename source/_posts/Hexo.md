title: Hexo的使用介绍
date: 2015-12-25 18:29:00
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
### 写文章

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
        toc: true # 生成目录
        author:
        comments:
        original:
        permalink: #指定链接
        ---

        以上是摘要
        <!--more-->

        以下是余下全文
```
### 写多种文章

```
    $ hexo new [layout] "postName" #新建文章
    [layout]：其中layout是可选参数，默认值为post。有哪些layout呢，请到 scaffolds 目录下查看，这些文件名称就是layout名称。当然你可以添加自己的layout，方法就是添加一个文件即可，同时你也可以编辑现有的layout，比如post的layout默认是 hexo\scaffolds\post.md
```
### 写页面（404）

```
    $ hexo new page "404"

    UUhike@UUhike-pc MINGW64 /d/Hexo/Hexo (master)
    $ hexo new page "404"
    INFO  Created: D:\Hexo\Hexo\source\404\index-1.md
```
```
title: 404 Not Found：该页无法显示
comments: false
permalink: /404
fancybox: false
---

<style type="text/css">
    .article-title {
        font-size: 2.1em;
    }
    strong a {
        color: #747474;
    }
    .share {
        display: none;
    }
    .player {
        margin-left: -10px;
    }
    .sign {
        text-align: right;
        font-style: italic;
    }
    #page-visit {
        display: none;
    }
    .center {
        text-align: center;
        height: 2.5em;
        font-weight: bold;
    }
    .search2 {
        height: 2.2em;
        font-size: 1em;
        width: 50%;
        margin: auto 24%;
        color: #727272;
        opacity: .6;
        border: 2px solid lightgray;
    }
    .search2:hover {
        opacity: 1;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.3)
        };
    .article-entry hr {
        margin: 0;
    }
    .pic {
        text-align: center;
        margin: 0;
    }
    .pic br {
        display: none;
    }
</style>

***

<div class="pic">
<img src="/resources/Mihawk-Wind.gif" title="Mihawk-Wind">
</div>

<p class="center">很抱歉，您所访问的地址并不存在: </p>

<p class="center"><a href="/">回主页</a> · <a href="/archives">所有文章</a> · <a href="/about">留言板</a></p>

<p class="center">可在边栏搜索框中对本站进行检索，以获取相关信息。</p>

<div style="text-align: center">
以下是博主喜欢的一些歌曲，可以听听，稍作休息~
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=320 height=330 src="http://music.163.com/outchain/player?type=0&id=112513213&auto=0&height=430"></iframe>
</div>

```

### 配置配置“多说”留言

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

### 发布博客内容
实现发布，前提是配置好，部署到Github前需要配置_config.yml文件。

```
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: github
  repository: git@github.com:zhchnchn/zhchnchn.github.io.git
  branch: master

```
更新的最新版本，可能会有Bug，自行百度，好像要修改type：git。
```
    $ hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）Hexo 会监视文件变动并自动更新，您无须重启服务器。

    $ hexo g #生成
    $ hexo generate #生成静态页面至public目录（最终上传这个文件到GitHub）

    $ hexo d == hexo deploy#部署
    $ hexo d #部署 # 可与hexo g合并为 hexo d -g

    $ hexo deploy -g
    $ hexo server -g # 生成默认文件群再执行,开启本地静态html服务器
```

### 主题的更改

```
1. 将Git Shell 切到/D/Hexo目录下，然后执行下面的命令，将pacman下载到 themes/pacman 目录下。

$ git clone https://github.com/A-limon/pacman.git themes/pacman
2. 修改你的博客根目录/D/Hexo下的config.yml配置文件中的theme属性，将其设置为pacman。

3. 更新pacman主题

$ cd themes/pacman
$ git pull

NOTE：先备份_config.yml 文件后再升级

主题：
    yilia
    $ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
    modernist
    $ git clone https://github.com/heroicyang/hexo-theme-modernist.git themes/modernist
    jacman
    $ git clone https://github.com/cnfeat/cnfeat.git themes/jacman
```


### 文章图片路径
Hexo如何方式图片，图片应该放置到哪里，不会应为上传而覆盖掉。然后把文章里的index.md删除，将文件存放在resource文件夹中间。

```
    发布页面
    $ hexo new page "name" # 新建一个页面，页面名称name

    UUhike@UUhike-pc MINGW64 /d/Hexo/Hexo (master)
    $ hexo new page "resoures"
    INFO  Created: D:\Hexo\Hexo\source\resoures\index.md
```

### RSS不显示

```
    安装RSS插件

    $ npm install hexo-generator-feed --save

    开启RSS功能

    编辑hexo/themes_config.yml，添加如下代码：

    rss: /atom.xml #rss地址  默认即可
```
### sitemap网站地图

```
1、安装插件：

$ npm install hexo-generator-sitemap --save
$ npm install hexo-generator-baidu-sitemap --save

2、在博客目录的hexo/_config.yml中添加如下代码：

# 自动生成sitemap编辑

sitemap:
path: sitemap.xml
baidusitemap:
path: baidusitemap.xml

3、hexo编译的时候会自动在根目录生成站点地图

    UUhike@UUhike-pc MINGW64 /d/Hexo/Hexo (master)
    $ npm install hexo-generator-sitemap --save
    npm WARN install Couldn't install optional dependency: Unsupported
    npm WARN install Couldn't install optional dependency: Unsupported
    hexo-site@0.0.0 D:\Hexo\Hexo
    └── hexo-generator-sitemap@1.0.1


    UUhike@UUhike-pc MINGW64 /d/Hexo/Hexo (master)
    $ npm install hexo-generator-baidu-sitemap --save
    npm WARN install Couldn't install optional dependency: Unsupported
    npm WARN install Couldn't install optional dependency: Unsupported
    hexo-site@0.0.0 D:\Hexo\Hexo
    └── hexo-generator-baidu-sitemap@0.1.2


    UUhike@UUhike-pc MINGW64 /d/Hexo/Hexo (master)
    $ hexo g
    INFO  Files loaded in 2.42 s
    INFO  Generated: baidusitemap.xml
    INFO  Generated: sitemap.xml
    INFO  2 files generated in 477 ms

```


### 创建instagram

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



### Wiki

聚沙成塔，记录碎片化信息，构筑个人知识体系













### Hexo文件备份

```
git-backup.

Install

if your hexo version is 2.x.x, you should install as follow:

$ npm install hexo-git-backup@0.0.91 --save
if version is 3.x.x, you should install as follow:

$ npm install hexo-git-backup --save
Update

if you install with --save, you must remove firstly when you update it.

$ npm remove hexo-git-backup
$ npm install hexo-git-backup --save
Configure

You should configure this plugin in _config.yml.

backup:
    type: git
    repository:
       github: git@github.com:xxx/xxx.git,branchName
       gitcafe: git@github.com:xxx/xxx.git,branchName
Using

hexo backup 
or

hexo b
Options

if you want to back up with your theme,just add theme: your theme name,your theme name in _config.yml.

backup:
    type: git
    theme: coney,landscape,xxx
    repository:
       github: git@github.com:xxx/xxx.git,branchName
       gitcafe: git@github.com:xxx/xxx.git,branchName
Attention: if you do as above, the dir themes/coney/.gitwill be removed

if you want DIY commit message, just add 'message: update xxx'.

backup:
    type: git
    message: update xxx
    repository:
       github: git@github.com:xxx/xxx.git,branchName
       gitcafe: git@github.com:xxx/xxx.git,branchName
Now you can backup all the blog!

Problems

You may get some troubles by your computer' permission。

Error: EISDIR, open

it is caused by permission. just do 'sudo hexo b'

sudo hexo b
```


