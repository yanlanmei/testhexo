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

```Text
grunt是前端工程化的先驱

gulp更自然基于流的方式连接任务

Webpack最年轻，擅长用于依赖管理，配置稍较复杂

推荐使用Gulp，Gulp基于nodejs中stream，效率更好语法更自然,不需要编写复杂的配置文件
```

## 安装前准备：

Gulp是基于 Node.js的，需要要安装 Node.js

### 为了确保依赖环境正确，我们先执行几个简单的命令检查。

```
luuman@luuman-PC MINGW64 ~
$ node -v

v5.3.0

Node是一个基于Chrome JavaScript V8引擎建立的一个解释器
检测Node是否已经安装，如果正确安装的话你会看到所安装的Node的版本号
```
### 接下来看看npm，它是 node 的包管理工具，可以利用它安装 gulp 所需的包

```
luuman@luuman-PC MINGW64 ~
$ npm -v

3.3.12

这同样能得到npm的版本号，装 Node 时已经自动安装了npm
```
### 开始全局安装Gulp

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

## 创建工程

### 演示项目目录结构

```
└─┬ src — 源文件:
	├──images
	├──scripts
	├──styles
├──build — 编译后文件输出到的生产文件夹:
├──images
├──scripts
├──styles


TestProject     (项目名称)
|–.git               通过git进行版本控制,项目自动生成这个文件
|–node_modules       组件包目录
|–dist               发布环境（编译自动生成的）
    |–css                 样式文件(style.css style.min.css)
    |–images              图片文件(压缩图片\合并后的图片)
    |–js                  js文件(main.js main.min.js)
    |–index.html          静态页面文件(压缩html)

|–src                开发环境
    |–sass                sass文件
    |–images              图片文件
    |–js                  js文件
    |–index.html          静态文件
|–gulpfile.js        gulp配置文件
|–package.json       依赖模块json文件,在项目目录下npm install会安装项目所有的依赖模块，简化项目的安装程序
```

### 创建package.json

我们先使用npm init来创建类似Nuget package的package.config一样的文件，这样我们就知道项目依赖哪些插件，而且我们不需要把插件提交到代码库，其它程序员只需要使用 npm install 就可以安装所有配置的插件

```
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (test) test                  //名称
version: (1.0.0) 1.0.0             //版本
description: test description      //描述
entry point: (index.js)            //
test command:                      //测试代码
git repository:                    //Git版本库
keywords:                          //关键词
author: luuman                     //作者
license: (ISC)                     //协议
About to write to F:\Gulp\test\package.json:

{
  "name": "test",
  "version": "1.0.0",
  "description": "test description",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "luuman",
  "license": "ISC"
}

Is this ok? (yes)

```

### 安装插件，加到项目依赖package.json中

npm install gulp --save-dev //将具体的gulp功能插件局部安装项目下

```
$ npm install gulp --save-dev

npm WARN deprecated graceful-fs@3.0.8: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
npm WARN deprecated lodash@1.0.2: lodash@<3.0.0 is no longer maintained. Upgrade to lodash@^4.0.0.
npm WARN deprecated graceful-fs@1.2.3: graceful-fs version 3 and before will fail on newer node releases. Please update to graceful-fs@^4.0.0 as soon as possible.
F:\Gulp\new
└─┬ gulp@3.9.1
```

npm install gulp-sass --save-dev //将具体的gulp功能插件局部安装项目下

```
$ npm install gulp-sass --save-dev
```

### 安装gulp功能插件依赖包

npm install gulp-jshint gulp-sass gulp-concat gulp-uglify gulp-rename--save-dev
gulp功能模块的文件会放在项目所在的目录的./node_modules 下


### 引入插件包

```
npm install

当package.json中已经有提示插件依赖包，node.js将会直接下载所有依赖插件包。
```

### 简单的功能：

| 插件 | 功能 |
|  ---- | ---- |
| gulp-imagemin:     | 压缩图片
| gulp-ruby-sass:    | 支持sass，安装此版本需要安装ruby
| gulp-minify-css:   | 压缩css
| gulp-jshint:       | 检查js
| gulp-uglify:       | 压缩js
| gulp-concat:       | 合并文件
| gulp-rename:       | 重命名文件
| gulp-htmlmin:      | 压缩html
| gulp-clean:        | 清空文件夹
| gulp-livereload:   | 服务器控制客户端同步刷新（需配合chrome插件LiveReload及tiny-lr）

#### gulp-jshint

```
luuman@luuman-PC MINGW64 /f/Gulp/new
$ npm install gulp-jshint --save-dev

F:\Gulp\new
├─┬ gulp@3.9.1
├─┬ gulp-jshint@2.0.0

npm WARN EPEERINVALID gulp-jshint@2.0.0 requires a peer of jshint@2.x but none was installed.
```

### 补充：的前端开发软件环境

```text
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