title: Gulp前端自动化
date: 2016-04-02 14:11:20
description: 
categories:
- HTML
tags:
- automation
toc: true
author:
comments:
original:
permalink: 
---

　　**Gulp前端自动化：**Gulp的高度集成化开发环境，释放了前端开发中大量时间，如css压缩、js压缩、错误检查、合并js、压缩图片、压缩html、模块构造等，只要你能想到的基本都可以通过Gulp插件去实现。

<!-- more -->

## 前端自动化的目的

在一个项目过程中，重复而枯燥的工作太多了……绳命就这样浪费了。
我们需要一个自动化的工作流程，让我们更专注于coding，而不是coding外的繁琐工作。于是Gulp应运而生。可以想像，如果在node环境下，一行命令搞定一个场景，So Cool…

然而通过了解，显然可看出Gulp

### 功能：

>1. 版本控制
2. 检查JS
3. 图片合并
4. 压缩CSS
5. 压缩JS
6. 编译SASS

### 目前最知名的构建工具： Gulp、Grunt、NPM + Webpack；

```
grunt是前端工程化的先驱

gulp更自然基于流的方式连接任务

Webpack最年轻，擅长用于依赖管理，配置稍较复杂

推荐使用Gulp，Gulp基于nodejs中stream，效率更好语法更自然,不需要编写复杂的配置文件
```

## 安装前准备：

Gulp是基于 Node.js的，需要要安装 Node.js

1、为了确保依赖环境正确，我们先执行几个简单的命令检查。

```
luuman@luuman-PC MINGW64 ~
$ node -v
v5.3.0

Node是一个基于Chrome JavaScript V8引擎建立的一个解释器
检测Node是否已经安装，如果正确安装的话你会看到所安装的Node的版本号
```
2、接下来看看npm，它是 node 的包管理工具，可以利用它安装 gulp 所需的包

```
luuman@luuman-PC MINGW64 ~
$ npm -v
3.3.12

这同样能得到npm的版本号，装 Node 时已经自动安装了npm
```
3、开始全局安装Gulp

```
luuman@luuman-PC MINGW64 ~
$ npm install -g gulp
npm WARN deprecated graceful-fs@3.0.8: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
npm WARN deprecated lodash@1.0.2: lodash@<3.0.0 is no longer maintained. Upgrade to lodash@^4.0.0.
npm WARN deprecated graceful-fs@1.2.3: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
C:\Users\luuman\AppData\Roaming\npm\gulp -> C:\Users\luuman\AppData\Roaming\npm\node_modules\gulp\bin\gulp.js
C:\Users\luuman\AppData\Roaming\npm
└─┬ gulp@3.9.1
  └─┬ gulp-util@3.0.7
    ├─┬ dateformat@1.0.12
    │ └─┬ meow@3.7.0
    │   └─┬ normalize-package-data@2.3.5
    │     └─┬ validate-npm-package-license@3.0.1
    │       └─┬ spdx-correct@1.0.2
    │         └── spdx-license-ids@1.2.1
    └─┬ fancy-log@1.2.0
      └── time-stamp@1.0.1
```

```
luuman@luuman-PC MINGW64 /l/Github
$ gulp -v
[18:39:18] CLI version 3.9.1

得到gulp的版本号，确认安装成功
```

## 工程创建

### 创建

创建一个文件目录，然后建立对应的文件夹

```
src — 源文件:
	images
	scripts
	styles
build — 编译后文件输出到的生产文件夹:
images
scripts
styles
```
### 引入依赖

npm install gulp --save-dev //将具体的gulp功能插件局部安装项目下

```
$ npm install gulp --save-dev
npm WARN deprecated graceful-fs@3.0.8: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
npm WARN deprecated lodash@1.0.2: lodash@<3.0.0 is no longer maintained. Upgrade to lodash@^4.0.0.
npm WARN deprecated graceful-fs@1.2.3: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
F:\Gulp\new
└─┬ gulp@3.9.1
  ├── archy@1.0.0
  ├─┬ chalk@1.1.3
  │ ├── ansi-styles@2.2.1
  │ ├── escape-string-regexp@1.0.5
  │ ├─┬ has-ansi@2.0.0
  │ │ └── ansi-regex@2.0.0
  │ ├── strip-ansi@3.0.1
  │ └── supports-color@2.0.0
  ├── deprecated@0.0.1
  ├─┬ gulp-util@3.0.7
  │ ├── array-differ@1.0.0
  │ ├── array-uniq@1.0.2
  │ ├── beeper@1.1.0
  │ ├─┬ dateformat@1.0.12
  │ │ ├── get-stdin@4.0.1
  │ │ └─┬ meow@3.7.0
  │ │   ├─┬ camelcase-keys@2.1.0
  │ │   │ └── camelcase@2.1.1
  │ │   ├── decamelize@1.2.0
  │ │   ├─┬ loud-rejection@1.3.0
  │ │   │ ├── array-find-index@1.0.1
  │ │   │ └── signal-exit@2.1.2
  │ │   ├── map-obj@1.0.1
  │ │   ├─┬ normalize-package-data@2.3.5
  │ │   │ ├── hosted-git-info@2.1.4
  │ │   │ ├─┬ is-builtin-module@1.0.0
  │ │   │ │ └── builtin-modules@1.1.1
  │ │   │ └─┬ validate-npm-package-license@3.0.1
  │ │   │   ├─┬ spdx-correct@1.0.2
  │ │   │   │ └── spdx-license-ids@1.2.1
  │ │   │   └─┬ spdx-expression-parse@1.0.2
  │ │   │     └── spdx-exceptions@1.0.4
  │ │   ├── object-assign@4.0.1
  │ │   ├─┬ read-pkg-up@1.0.1
  │ │   │ ├─┬ find-up@1.1.2
  │ │   │ │ ├── path-exists@2.1.0
  │ │   │ │ └─┬ pinkie-promise@2.0.0
  │ │   │ │   └── pinkie@2.0.4
  │ │   │ └─┬ read-pkg@1.1.0
  │ │   │   ├─┬ load-json-file@1.1.0
  │ │   │   │ ├── graceful-fs@4.1.3
  │ │   │   │ ├─┬ parse-json@2.2.0
  │ │   │   │ │ └─┬ error-ex@1.3.0
  │ │   │   │ │   └── is-arrayish@0.2.1
  │ │   │   │ ├── pify@2.3.0
  │ │   │   │ └── strip-bom@2.0.0
  │ │   │   └── path-type@1.1.0
  │ │   ├─┬ redent@1.0.0
  │ │   │ ├─┬ indent-string@2.1.0
  │ │   │ │ └─┬ repeating@2.0.0
  │ │   │ │   └─┬ is-finite@1.0.1
  │ │   │ │     └── number-is-nan@1.0.0
  │ │   │ └── strip-indent@1.0.1
  │ │   └── trim-newlines@1.0.0
  │ ├─┬ fancy-log@1.2.0
  │ │ └── time-stamp@1.0.1
  │ ├─┬ gulplog@1.0.0
  │ │ └── glogg@1.0.0
  │ ├─┬ has-gulplog@0.1.0
  │ │ └── sparkles@1.0.0
  │ ├── lodash._reescape@3.0.0
  │ ├── lodash._reevaluate@3.0.0
  │ ├── lodash._reinterpolate@3.0.0
  │ ├─┬ lodash.template@3.6.2
  │ │ ├── lodash._basecopy@3.0.1
  │ │ ├── lodash._basetostring@3.0.1
  │ │ ├── lodash._basevalues@3.0.0
  │ │ ├── lodash._isiterateecall@3.0.9
  │ │ ├─┬ lodash.escape@3.2.0
  │ │ │ └── lodash._root@3.0.1
  │ │ ├─┬ lodash.keys@3.1.2
  │ │ │ ├── lodash._getnative@3.9.1
  │ │ │ ├── lodash.isarguments@3.0.8
  │ │ │ └── lodash.isarray@3.0.4
  │ │ ├── lodash.restparam@3.6.1
  │ │ └── lodash.templatesettings@3.1.1
  │ ├─┬ multipipe@0.1.2
  │ │ └─┬ duplexer2@0.0.2
  │ │   └── readable-stream@1.1.13
  │ ├── object-assign@3.0.0
  │ ├── replace-ext@0.0.1
  │ ├─┬ through2@2.0.1
  │ │ ├─┬ readable-stream@2.0.6
  │ │ │ ├── core-util-is@1.0.2
  │ │ │ ├── inherits@2.0.1
  │ │ │ ├── isarray@1.0.0
  │ │ │ ├── process-nextick-args@1.0.6
  │ │ │ ├── string_decoder@0.10.31
  │ │ │ └── util-deprecate@1.0.2
  │ │ └── xtend@4.0.1
  │ └─┬ vinyl@0.5.3
  │   ├── clone@1.0.2
  │   └── clone-stats@0.0.1
  ├── interpret@1.0.0
  ├─┬ liftoff@2.2.1
  │ ├── extend@2.0.1
  │ ├─┬ findup-sync@0.3.0
  │ │ └─┬ glob@5.0.15
  │ │   ├── inflight@1.0.4
  │ │   ├── minimatch@3.0.0
  │ │   └── path-is-absolute@1.0.0
  │ ├── flagged-respawn@0.3.2
  │ ├── rechoir@0.6.2
  │ └── resolve@1.1.7
  ├── minimist@1.2.0
  ├─┬ orchestrator@0.3.7
  │ ├─┬ end-of-stream@0.1.5
  │ │ └─┬ once@1.3.3
  │ │   └── wrappy@1.0.1
  │ ├── sequencify@0.0.7
  │ └── stream-consume@0.1.0
  ├── pretty-hrtime@1.0.2
  ├── semver@4.3.6
  ├─┬ tildify@1.1.2
  │ └── os-homedir@1.0.1
  ├─┬ v8flags@2.0.11
  │ └── user-home@1.1.1
  └─┬ vinyl-fs@0.3.14
    ├── defaults@1.0.3
    ├─┬ glob-stream@3.1.18
    │ ├── glob@4.5.3
    │ ├─┬ glob2base@0.0.12
    │ │ └── find-index@0.1.1
    │ ├─┬ minimatch@2.0.10
    │ │ └─┬ brace-expansion@1.1.3
    │ │   ├── balanced-match@0.3.0
    │ │   └── concat-map@0.0.1
    │ ├── ordered-read-streams@0.1.0
    │ ├─┬ through2@0.6.5
    │ │ └── readable-stream@1.0.33
    │ └── unique-stream@1.0.0
    ├─┬ glob-watcher@0.0.6
    │ └─┬ gaze@0.5.2
    │   └─┬ globule@0.1.0
    │     ├─┬ glob@3.1.21
    │     │ ├── graceful-fs@1.2.3
    │     │ └── inherits@1.0.2
    │     ├── lodash@1.0.2
    │     └─┬ minimatch@0.2.14
    │       ├── lru-cache@2.7.3
    │       └── sigmund@1.0.1
    ├── graceful-fs@3.0.8
    ├─┬ mkdirp@0.5.1
    │ └── minimist@0.0.8
    ├─┬ strip-bom@1.0.0
    │ ├── first-chunk-stream@1.0.0
    │ └── is-utf8@0.2.1
    ├─┬ through2@0.6.5
    │ └─┬ readable-stream@1.0.33
    │   └── isarray@0.0.1
    └─┬ vinyl@0.4.6
      └── clone@0.2.0

```

### 安装gulp功能插件依赖包

npm install gulp-jshint gulp-sass gulp-concat gulp-uglify gulp-rename--save-dev
gulp功能模块的文件会放在项目所在的目录的./node_modules 下

### 简单的功能：

gulp-jshint
gulp-sass
gulp-concat
gulp-uglify
- 检查Javascript
- 编译Sass文件
- 合并Javascript
- 压缩合并并重命名Javascript

#### gulp-jshint

luuman@luuman-PC MINGW64 /f/Gulp/new
$ npm install gulp-jshint --save-dev
F:\Gulp\new
├─┬ gulp@3.9.1
│ └─┬ vinyl-fs@0.3.14
│   ├─┬ glob-stream@3.1.18
│   │ ├── minimatch@2.0.10
│   │ └─┬ through2@0.6.5
│   │   └── readable-stream@1.0.33
│   └─┬ through2@0.6.5
│     └── readable-stream@1.0.33
├─┬ gulp-jshint@2.0.0
│ ├── lodash@3.10.1
│ ├── minimatch@2.0.10
│ ├─┬ rcloader@0.1.2
│ │ ├── lodash@2.4.2
│ │ └─┬ rcfinder@0.1.8
│ │   └── lodash@2.4.2
│ └─┬ through2@0.6.5
│   └── readable-stream@1.0.33
└── UNMET PEER DEPENDENCY jshint@2.x

npm WARN EPEERINVALID gulp-jshint@2.0.0 requires a peer of jshint@2.x but none w                   as installed.


### 补充：的前端开发软件环境

```
Node.Js、NPM、Ruby、Java        基础环境
Sublime + 插件                  用于编写前端代码
Chrome、Firefox + Firebug       浏览器
Internet Explorer               进行兼容测试和预览页面UI、动画效果和交互功能
Node.js+Gulp                    进行前端自动化构建、JS语法验证、CSS压缩，图片压缩等；
Koala                           实时编译Less、Sass、Compass、CoffeeScript;
Github                          存储自己的代码库 、git或SVN用于版本控制和团队Code Review
Tomcat、DedeAMPZ、MAMP          进行简单运行环境演示
Photoshop CC 切图 + Sprites     合并小图标
XMind                           画出清晰的工作或业务逻辑思维图
```

```
新建gulpfile.js 配置文件放在项目根目录下

演示项目目录结构
testProject     (项目名称)
|–.git            通过git进行版本控制,项目自动生成这个文件
|–node_modules    组件包目录
|–dist            **发布环境**（编译自动生成的）
    |–css         样式文件(style.css style.min.css)
    |–images  图片文件(压缩图片\合并后的图片)
    |–js      js文件(main.js main.min.js)
    |–index.html  静态页面文件(压缩html)
|–src             **开发环境**
    |–sass                sass文件
    |–images              图片文件
    |–js                  js文件
    |–index.html      静态文件
|–gulpfile.js             gulp配置文件
|–package.json            依赖模块json文件,在项目目录下npm install会安装项目所有的依赖模块，简化项目的安装程序
```

```
现在，项目文件夹都建好，组件也安装完毕了，我们需要编写gulpfile.js文件以指定gulp需要为我们完成什么任务。

gulpfile.js内容如下：

// 引入gulp
var gulp = require('gulp');

// 引入组件
var jshint = require('gulp-jshint');//检查js
var sass   = require('gulp-sass');  //编译Sass
var concat = require('gulp-concat');//合并
var uglify = require('gulp-uglify');//uglify 组件（用于压缩 JS）
var rename = require('gulp-rename');//重命名

// 检查js脚本的任务
gulp.task('lint', function() {
    gulp.src('./js/*.js') //可配置你需要检查脚本的具体名字。
        .pipe(jshint())
        .pipe(jshint.reporter('default'));
});

// 编译Sass
gulp.task('sass', function() {
    gulp.src('./scss/*.scss')
        .pipe(sass())
        .pipe(gulp.dest('./css'));//dest()写入文件
});

// 合并，压缩js文件
// 找到 js/ 目录下的所有 js 文件，压缩，重命名，最后将处理完成的js存放在 dist/js/ 目录下
gulp.task('scripts', function() {
    gulp.src('./js/*.js')
        .pipe(concat('all.js'))
        .pipe(gulp.dest('./dist'))
        .pipe(rename('all.min.js'))
        .pipe(uglify())
        .pipe(gulp.dest('./dist'));

        console.log('gulp task is done');//自定义提醒信息
});
```

.... // 其他任务类似

// 定义默认任务,执行gulp会自动执行的任务
gulp.task('default', function(){
    gulp.run('lint', 'sass', 'scripts');

    // 监听js文件变化，当文件发生变化后会自动执行任务
    gulp.watch('./js/*.js', function(){
        gulp.run('lint','scripts');
    });
});

```
现在，回到命令行窗口，可以直接运行gulp任务了。

gulp

这将执行定义的default任务，就和以下的命令式同一个意思

gulp default

当然，我们可以运行在gulpfile.js中定义的任意任务，比如，现在单独运行sass任务：

gulp sass
```

### 编译会显示Finished,如果你的JS有什么不好的地方它会提醒，避免一些不必要的错误，十分贴心

```
常见提醒：
1.禁止在同一行声明多个变量。
2.请使用 ===/!==来比较true/false或者数值
3.使用对象字面量替代new Array这种形式
4.不要使用全局函数。
5.Switch语句必须带有default分支
6.函数不应该有时候有返回值，有时候没有返回值。
7.For循环必须使用大括号
8.If语句必须使用大括号
9.for-in循环中的变量 应该使用var关键字明确限定作用域，从而避免作用域污染。
```
### gulp的插件数量很多，后面还可以根据自己的需要进行添加任务

```
常用的gulp插件参考
gulp-imagemin:      压缩图片
gulp-ruby-sass:     支持sass，安装此版本需要安装ruby
gulp-minify-css:    压缩css
gulp-jshint:        检查js
gulp-uglify:        压缩js
gulp-concat:        合并文件
gulp-rename:        重命名文件
gulp-htmlmin:       压缩html
gulp-clean:         清空文件夹
gulp-livereload:    服务器控制客户端同步刷新（需配合chrome插件LiveReload及tiny-lr）
```


## 前端自动化的目的

相关资料：

[Gruntjs](http://gruntjs.com "The JavaScript Task Runner")
[Grunt安装及配合组件构建前端开发一体化](http://www.dbpoo.com/getting-started-with-grunt/ "")
[grunt前端打包——css篇](http://www.php100.com/html/it/qianduan/2015/0115/8377.html: "")
[SourceTree](http: "")

[SourceTree](http: "")
[SourceTree](http: "")
[SourceTree](http: "")
[SourceTree](http: "")


http://markyun.github.io/2015/The-front-end-code-build-automated-build-environment/

http://www.cnblogs.com/cnblogsfans/p/5104450.html