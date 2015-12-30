title: 使用GitHub搭建Hexo博客
date: 2015-12-21 18:29:00
description: 来到GitHub这么长时间，才开始真真的了解GitHub，这个国外的代码托管平台，充满着大牛的身影。
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
来到GitHub这么长时间，才开始真真的了解GitHub，这个国外的代码托管平台，充满着大牛的身影。
国内也有不多少的代码托管平台，本文将就用GitHub的GitHub Pages 功能来搭建，我的个性博客，[hexo](2)是由Node.js驱动的一款快速、简单且功能强大的博客框架。
比起WordPress，hexo的搭建更加简洁，配合上markdown的使用，更加便捷的管理自己的学习文档。
<!--more-->
>1. 为什么选择[GitHub Pages](1)
1、[GitHub Pages](1)有免费的代码托管空间，资料自己管理，保存可靠；
2、学着用 GitHub，享受 GitHub 的便利，上面有很多大牛，眼界会开阔很多；
3、顺便理解 GitHub 工作原理，最好的团队协作流程；
4、GitHub建立私有仓库才会收费，所以会有很多开源代码。
>2. [GitHub Pages](1)是什么
应用GitHub Pages创建属于自己的个人博客，GitHub将提供免费的空间。
GitHub提供的域名（用户名+github+io）,在Repository name对应处填写资源名，其需要使用自己的用户名，每个用户名下面只能建立一个，并且资源命名必须符合这样的规则username/username.github.io，之后勾选下面的"Initialize this repository with a README" 。
>3. [hexo](2)出自何人
hexo出自台湾大学生 tommy351 之手，是一个基于Node.js的静态博客程序，其编译上百篇文字只需要几秒。hexo生成的静态网页可以直接放到GitHub Pages，BAE，SAE等平台上。

# 二、安装准备
>## 环境搭建：
1. [Node.js](http://nodejs.org/)：下载[地址](https://nodejs.org/en/)
2. [Git](http://git-scm.com/)：下载[地址](https://git-scm.com/download/win)
3. [Sublime](http://www.sublimetext.com/)：下载[地址](http://www.sublimetext.com/2)

>## 安装Node 
到 Node.js 官网下载相应平台的 最新版本 ，一路安装即可。我用的是 node-v0.10.22-x86.msi

>## 安装Git 
Git的客户端很多，我用的是 msysgit ，喜欢用绿色版本 Portable application for official Git for Windows 1.8.4 ，下载下来设置一下环境变量即可，Git_HOME，%Git_HOME%\bin之类的，不多说。

>## 安装Sublime
Sublime Text 2 在这里仅仅作为一个文本编辑器使用，支持各种编程语言和文件格式，当然也支持Markdown语法，实在是个不可多得的练码奇才。喜欢追鲜的也可以尝试处于beta版本的 Sublime Text 3 。


# 三、GitHub注册与配置

## 1、注册：
访问：[GitHub](0)，注册你的username和邮箱，邮箱十分重要，GitHub上很多通知都是通过邮箱的。注册过程比较简单，详细也可以看：

## 2、配置和使用Github
以下教程主要参考beiyuu的[《使用Github Pages建独立博客》](http://beiyuu.com/github-pages/)写成。

## 3、配置SSH keys
我们如何让本地git项目与远程的github建立联系呢？用SSH keys。
打开Git Bash工具，执行以下操作

## 检查SSH keys的设置

```
    首先我们需要检查你电脑上现有的ssh key：

    $ cd ~/. ssh 检查本机的ssh密钥

如果提示：No such file or directory 说明你是第一次使用git。

    生成新的SSH Key：

    $ ssh-keygen -t rsa -C "邮件地址@youremail.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key 
    (/Users/your_user_directory/.ssh/id_rsa):<回车就好>
```
注意1: 此处的邮箱地址，你可以输入自己的邮箱地址；
注意2: 此处的「-C」的是大写的「C」

    然后系统会要你输入密码：
    Enter passphrase (empty for no passphrase):<输入加密串>
    Enter same passphrase again:<再次输入加密串>

在回车中会提示你输入一个密码，这个密码会在你提交项目时使用，如果为空的话提交项目时则不用输入。这个设置是防止别人往你的项目里提交内容。

注意：输入密码的时候没有*字样的，你直接输入就可以了。

最后看到这样的界面，就成功设置ssh key了：
![](http://upload-images.jianshu.io/upload_images/1064727-9b74c870ed3f3710.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 添加SSH Key到GitHub

在本机设置SSH Key之后，需要添加到GitHub上，以完成SSH链接的设置。
>1. 打开本地C:\Documents and Settings\Administrator.ssh\id_rsa.pub文件。此文件里面内容为刚才生成人密钥。如果看不到这个文件，你需要设置显示隐藏文件。准确的复制这个文件的内容，才能保证设置的成功。
2. 登陆github系统。点击右上角的 Account Settings--->SSH Public keys ---> add another public keys
3. 把你本地生成的密钥复制到里面（key文本框中）， 点击 add key 就ok了

## 测试

可以输入下面的命令，看看设置是否成功，git@github.com的部分不要修改：

    $ ssh -T git@github.com

如果是下面的反馈：

    The authenticity of host 'github.com (207.97.227.239)' can't be established.
    RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
    Are you sure you want to continue connecting (yes/no)?

不要紧张，输入yes就好，然后会看到：

    Hi cnfeat! You've successfully authenticated, 
    but GitHub does not provide shell access.

设置用户信息：
>现在你已经可以通过SSH链接到GitHub了，还有一些个人信息需要完善的。
Git会根据用户的名字和邮箱来记录提交。GitHub也是用这些信息来做权限的处理，输入下面的代码进行个人信息的设置，把名称和邮箱替换成你自己的，名字必须是你的真名，而不是GitHub的昵称。

    $ git config --global user.name "cnfeat"//用户名
    $ git config --global user.email "cnfeat@gmail.com"//填写自己的邮箱

SSH Key配置成功，本机已成功连接到github。


# 四、Hexo主题

#### Hexo

Hexo的作者是[tommy351](https://github.com/tommy351/hexo)，根据[官方介绍](http://hexo.io/docs/index.html)，Hexo是一个简单、快速、强大的博客发布工具，支持Markdown格式。hexo的主题列表 [Hexo Themes](http://github.com/tommy351/hexo/wiki/Themes)。 我比较喜欢 [pacman](http://github.com/A-limon/pacman) ， [modernist](http://github.com/heroicyang/hexo-theme-modernist) 、 [ishgo](http://github.com/DavidKk/Hexo.ishgo) ， [raytaylorism](http://github.com/raytaylorlin/hexo-theme-raytaylorism) 。 



>1、安装Hexo

打开Git Bash工具（前提确保Node.js已经安装，环境配置OK）

    $ npm install -g hexo

>2、部署Hexo

```
在我的电脑中建立一个名字叫「Hexo」的文件夹，然后在此文件夹中右键打开Git Bash。

    $ hexo init

    如果无法使用右击“Git Bash”，则可以切换到指定目录

    UUhike@UUhike-pc MINGW64 ~
    $ cd j:/github/hexo
    UUhike@UUhike-pc MINGW64 /j/github/hexo

Hexo随后会自动在目标文件夹建立网站所需要的所有文件。
现在我们已经搭建起本地的hexo博客了，执行以下命令(在H:\hexo)，然后到浏览器输入localhost:4000看看。




    $ hexo generate #生成静态页面至public目录（最终上传这个文件到GitHub）

    $ hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
```
>3、复制cnfeat的主题

以下进入复制主题环节，如果那一步出现问题，或者修改后没有显示修改的结果，建议来来一个，再看看，可以解决很多问题。

```
    $ hexo clean

    $ hexo generate #生成静态页面至public目录（最终上传这个文件到GitHub）

    $ hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）

    建立了Hexo文件，复制我的主题了到themes文件夹中
    yilia
    $ git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
    modernist
    $ git clone https://github.com/heroicyang/hexo-theme-modernist.git themes/modernist
    jacman
    $ git clone https://github.com/cnfeat/cnfeat.git themes/jacman
```


>4、启用cnfeat的主题

修改Hexo目录下的config.yml配置文件中的theme属性，将其设置为jacman。同时请设置stylus属性中的compress值为true。
theme: jacman

注意：Hexo有两个config.yml文件，一个在根目录，一个在theme下，此时修改的是在根目录下的。

    更新主题

    $ cd themes/jacman
    $ git pull

注意：为避免出错，请先备份你的_config.yml 文件后再升级
本地查看调试

```
    $ hexo g #生成
    $ hexo s #启动本地服务，进行文章预览调试

    或者直接作用组合命令

    $ hexo deploy -g
    $ hexo server -g

    简写：

    hexo n == hexo new
    hexo g == hexo generate
    hexo s == hexo server
    hexo d == hexo deploy
```
>4、浏览器中查看效果

浏览器输入[http://localhost:4000](http://localhost:4000) ，查看搭建效果。此后的每次变更_config.yml文件或者上传文件都可以先用此命令调试，非常好用，尤其是当你想调试出自己想要的主题时。

#进阶篇：Hexo设置

网站搭建完成后，就可以根据自己爱好来对Hexo生成的网站进行设置了，对整站的设置，只要修改项目目录的hexo/_config.yml就可以了，这是我的设置，可供参考。

>默认目录结构：

```
    .
    ├── .deploy
    ├── public
    ├── scaffolds
    ├── scripts
    ├── source
    |   ├── _drafts
    |   └── _posts
    ├── themes
    ├── _config.yml
    └── package.json
```
>hexo/_config.yml

```
    # Hexo Configuration
    ## Docs: http://hexo.io/docs/configuration.html
    ## Source: https://github.com/tommy351/hexo/

    # Site #整站的基本信息
    title: 1000 words a Day #网站标题
    subtitle: Writing 1000 Words a Day Changes My Life #网站副标题
    description: 学习总结 思考感悟 知识管理 #网站描述
    author:  cnFeat #网站作者，在下方显示
    email: cnFeat@gmail.com #联系邮箱
    language: zh-CN #主题实际的文件名称

    # URL
    ## If your site is put in a subdirectory
    url: http://www.cnfeat.com #你的域名
    root: /
    permalink: :year/:month/:day/:title/
    tag_dir: tags
    archive_dir: archives
    category_dir: categories
    code_dir: downloads/code

    # Directory
    source_dir: source
    public_dir: public

    # Writing
    new_post_name: :title.md # File name of new posts
    default_layout: post
    auto_spacing: false # Add spaces between asian characters and western characters
    titlecase: false # Transform title into titlecase
    external_link: true # Open external links in new tab
    max_open_file: 100
    multi_thread: true
    filename_case: 0
    render_drafts: false
    post_asset_folder: false
    highlight:
    enable: true
    line_number: true
    tab_replace:

    # Category & Tag
    default_category: uncategorized
    category_map:
    tag_map:

    # Archives
    ## 2: Enable pagination
    ## 1: Disable pagination
    ## 0: Fully Disable
    archive: 2
    category: 2
    tag: 2

    # Server
    ## Hexo uses Connect as a server
    ## You can customize the logger format as defined in
    ## http://www.senchalabs.org/connect/logger.html
    port: 4000
    server_ip: 0.0.0.0
    logger: false
    logger_format:

    # Date / Time format
    ## Hexo uses Moment.js to parse and display date
    ## You can customize the date format as defined in
    ## http://momentjs.com/docs/#/displaying/format/
    date_format: YYYY-MM-DD
    time_format: H:mm:ss

    # Pagination
    ## Set per_page to 0 to disable pagination
    per_page: 15 #每页15篇文章
    pagination_dir: page

    # Disqus #社会化评论disqus，我使用多说，在主题中配置
    disqus_shortname:

    # Extensions
    ## Plugins: https://github.com/tommy351/hexo/wiki/Plugins
    ## Themes: https://github.com/tommy351/hexo/wiki/Themes
    theme: jacman
    exclude_generator:
    Plugins:
    - hexo-generator-feed
    - hexo-generator-sitemap

    #sitemap
    sitemap:
    path: sitemap.xml

    #Feed Atom
    feed:
    type: atom
    path: atom.xml
    limit: 20

    # Markdown
    ## https://github.com/chjj/marked
    markdown:
    gfm: true
    pedantic: false
    sanitize: false
    tables: true
    breaks: true
    smartLists: true
    smartypants: true

    # Stylus
    stylus:
    compress: false

    # Deployment
    ## Docs: http://hexo.io/docs/deployment.html
    deploy:
    type: github
    repository: https://github.com/cnfeat/cnfeat.github.io.git
    branch: master  
```

修改局部页面

页面展现的全部逻辑都在每个主题中控制，源代码在hexo\themes\主题名称\中：
>hexo\themes\

```
├── languages  #多语言
|   ├── default.yml#默认语言
|   └── zh-CN.yml  #中文语言
├── layout #布局，根目录下的*.ejs文件是对主页，分页，存档等的控制
|   ├── _partial   #局部的布局，此目录下的*.ejs是对头尾等局部的控制
|   └── _widget#小挂件的布局，页面下方小挂件的控制
├── source #源码
|   ├── css#css源码 
|   |   ├── _base  #*.styl基础css
|   |   ├── _partial   #*.styl局部css
|   |   ├── fonts  #字体
|   |   ├── images #图片
|   |   └── style.styl #*.styl引入需要的css源码
|   ├── fancybox   #fancybox效果源码
|   └── js #javascript源代码
├── _config.yml#主题配置文件
└── README.md  #用GitHub的都知道
```

主题文档的配置
>hexo\themes/_config.yml

```
    # Header
    menu:
      主页: /
      所有文章: /archives
      # 随笔: /tags/随笔

    # SubNav
    subnav:
      github: "#"
      weibo: "#"
      rss: "#"
      zhihu: "#"
      #douban: "#"
      #mail: "#"
      #facebook: "#"
      #google: "#"
      #twitter: "#"
      #linkedin: "#"

    rss: /atom.xml

    # Content
    excerpt_link: more
    fancybox: true
    mathjax: true

    # Miscellaneous
    google_analytics: ''
    favicon: /favicon.png

    #你的头像url
    avatar: ""
    #是否开启分享
    share: true
    #是否开启多说评论，填写你在多说申请的项目名称 duoshuo: duoshuo-key（http://duoshuo-key.duoshuo.com/）
    #若使用disqus，请在博客config文件中填写disqus_shortname，并关闭多说评论
    duoshuo: true
    #是否开启云标签
    tagcloud: true

    #是否开启友情链接
    #不开启——
    #friends: false
    #开启——
    friends:
      奥巴马的博客: http://localhost:4000/
      卡卡的美丽传说: http://localhost:4000/
      本泽马的博客: http://localhost:4000/
      吉格斯的博客: http://localhost:4000/
      习大大大不同: http://localhost:4000/
      托蒂的博客: http://localhost:4000/

    #是否开启“关于我”。
    #不开启——
    #aboutme: false
    #开启——
    aboutme: 我是谁，我从哪里来，我到哪里去？我就是我，是颜色不一样的吃货…
```

发表新文章

#用hexo发表新文章

```
    $ hexo n #写文章 
    其中my new post为文章标题，执行命令后。
    会在项目\source_posts中生成my new post.md文件，用编辑器打开编写即可。

    当然，也可以直接在\source_posts中新建一个md文件，我就是这么做的。

写完后，推送到服务器上，执行

    $ hexo g #生成
    $ hexo d #部署 # 可与hexo g合并为 hexo d -g

##用Hexo发表文章的Markdown语法
使用jacman或pacman主题，建议按此标准语法写：

    title: postName #文章页面上的显示名称，可以任意修改，不会出现在URL中
    date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
    categories: example #分类
    tags: [tag1,tag2,tag3] #文章标签，可空，多标签请用格式，注意:后面有个空格
    description: 附加一段文章摘要，字数最好在140字以内。
    ---

    以下正文
```
>写文章

```
     hexo new [layout] "postName" #新建文章

其中layout是可选参数，默认值为post。
有哪些layout呢，请到 scaffolds 目录下查看，
这些文件名称就是layout名称。
当然你可以添加自己的layout，方法就是添加一个文件即可，
同时你也可以编辑现有的layout，比如post的layout默认是 hexo\scaffolds\post.md

    title: { { title } }
    date: { { date } }
    tags:
    ---
```
请注意，大括号与大括号之间我多加了个空格，否则会被转义，不能正常显示。
我想添加categories，以免每次手工输入，只需要修改这个文件添加一行，如下：

    title: { { title } }
    date: { { date } }
    categories: 
    tags: 
    ---
postName是md文件的名字，同时也出现在你文章的URL中，postName如果包含空格，必须用"将其包围，postName可以为中文。

注意，所有文件：后面都必须有个空格，不然会报错。
看一下刚才生成的文件 hexo\source\_posts\postName.md ，内容如下：

    title: postName #文章页面上的显示名称，可以任意修改，不会出现在URL中
    date: 2013-12-02 15:30:16 #文章生成时间，一般不改，当然也可以任意修改
    categories: #文章分类目录，可以为空，注意:后面有个空格
    tags: #文章标签，可空，多标签请用格式[tag1,tag2,tag3]，注意:后面有个空格
    ---
这里开始使用markdown格式输入你的正文。
接下来，你就可以用喜爱的编辑器尽情书写你的文章。关于markdown语法，可以参考我的文章 Markdown简明语法 。

>fancybox 

可能有人对这个 Reading 页面中图片的 fancybox 效果感兴趣，这个是怎么做的呢。 
很简单，只需要在你的文章*.md文件的头上添加 photos 项即可，然后一行行添加你要展示的照片：

    layout: photo
    title: 我的阅历
    date: 2085-01-16 07:33:44
    tags: [hexo]
    photos:
    - http://bruce.u.qiniudn.com/2013/11/27/reading/photos-0.jpg
    - http://bruce.u.qiniudn.com/2013/11/27/reading/photos-1.jpg

经过测试，文件头上的 layout: photo 可以省略。
不想每次都手动添加怎么办？同样的，打开您的 hexo\scaffolds\photo.md

    layout: { { layout } }
    title: { { title } }
    date: { { date } }
    tags: 
    photos: 
    - 
    ---
然后每次可以执行带layout的new命令生成照片文章：

     hexo new photo "photoPostName" #新建照片文章

>description 

markdown文件头中也可以添加description，以覆盖全局配置文件中的description内容，请参考下文 _config.yml 的介绍。
```
    title: title #文章标题
    date: 2015-02-05 12:47:44 #文章生成时间
    categories: #文章分类目录 可以省略
    tags: [博客,Hexo,建站]
    description: #你对本页的描述 可以省略
    toc: true #生成目录

   ---
   
   hexo默认会处理全部markdown和html文件，
   如果不想让hexo处理你的文件，可以在文件头中加入layout: false。

   文章摘要 
   在需要显示摘要的地方添加如下代码即可：

以上是摘要
   <!--more-->

以下是余下全文
   more以上内容即是文章摘要，在主页显示.
   more以下内容点击『> Read More』链接打开全文才显示。
```
hexo中所有文件的编码格式均是UTF-8。


>自定义页面

    执行new page命令

    hexo new page "about"

    在 *hexo\source\* 下会生成 *about* 目录，
    里面有个index.md，直接编辑就可以了，
    然后在主题的 *_config.yml* 中将其配置显示出来。 

    上述步骤，也可以手工生成，在 *hexo\source\* 下手工新建
     *about* 和 *index.md* 也是完全等价的。

    因为markdown对table的支持不好，我是在about中直接
    建立index.html，里面书写页面内容，hexo会帮你加上头和尾。


为什么我的博客有目录？

>安装插件
添加sitemap和feed插件

    $ npm install hexo-generator-sitemap
    $ npm install hexo-generator-feed
修改_config.yml，增加以下内容

    # Extensions
    Plugins:
    - hexo-generator-feed
    - hexo-generator-sitemap

    #Feed Atom
    feed:
      type: atom
      path: atom.xml
      limit: 20

    #sitemap
    sitemap:
      path: sitemap.xml
    Hexo上传README文件

>统计

因Google Analytics偶尔被墙，故用百度统计，以 *modernist* 主题为例，介绍如何添加。 编辑文件 *hexo\themes\modernist\_config.yml* ，增加配置选项：

    baidu_tongji: true

    新建文件 *hexo\themes\modernist\layout\_partial\baidu_tongji.ejs* ，内容如下：
    
    <% if (theme.baidu_tongji){ %><script type="text/javascript">
    #你的百度统计代码
    </script><% } %>

>换机器

你要保留好自己的博客源码。换机器写博客，就只能使用各种网盘的同步功能，或者你把你的站点源文件提交到某代码托管服务器。另外，貌似这篇很牛逼， [Hexo 服务器端布署及 Dropbox 同步](http://lucifr.com/2013/06/02/hexo-on-cloud-with-dropbox-and-vps/) 。

我的办法是这样的，先在一个目录下做好Node+Git+Hexo的绿色环境，写个 hexos.bat 可以一键启动hexo工作台，把整个目录用Dropbox同步，这样随便在办公室或家的任何笔记本台式机都可以写博客，也不用处理什么文件拷贝备份的事情，非常爽。


## 参考资料：
[hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)
[如何搭建一个独立博客——简明Github Pages与Hexo教程](http://www.jianshu.com/p/05289a4bc8b2#)
[]()

[0][GitHub](https://github.com/)
[1][GitHub Pages](https://pages.github.com/)
[2][hexo](http://zespia.tw/hexo/)