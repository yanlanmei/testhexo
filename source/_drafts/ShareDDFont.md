滴滴Webapp分享

今天分享的嘉宾和内容是：

黄轶，现就职于滴滴出行公共FE团队，前端技术专家。计算机专业硕士，2012年毕业于北京科技大学，曾任职百度。擅长前端自动化、工程化，前端架构等方向。业余时间写了一些逼近iOS原生体验的移动端picker组件，通用的帧动画库，好玩的h5小游戏（https://github.com/ustbhuangyi）。喜欢关注业界一些新技术，乐于分享，热爱开源。对代码有洁癖，追求高质量的代码。
【2016年】【8月】【前端之巅】【滴滴公共FE团队技术开放月】，一连三场分享活动，今天是第二场分享，将和大家分享滴滴WebApp实践经验。
1. WebApp首页技术架构
需求分析

（1）滴滴多条业务线在一个 WebApp 页面里运行，业务线之间互不影响。

（2）业务线发单流程基本一致，部分业务线支持自定义化。

（3）业务线可以独立自主迭代上线，不需要公共团队的参与。

（4）新业务线可以快速接入首页。
解决方案
（1）每个业务线提供自已的 biz.js，首页加载的时候会异步请求这些 JS 文件。
（2）公共提供全局的 dd.registerBiz(option) 方法，供业务线 biz.js 调用，同时在 option 里提供 init、onEnter、onExit、orderRecover 等钩子函数，业务线的代码通过调用 dd.registerBiz 方法完成接入。
（3）把页面拆分成多个区块，有一些公共区块如一级导航菜单和地址选择区块；也有一些业务线区块如 ETA 区块、发单区块、自定义区块等。公共会在业务线区块下根据 registerBiz 注册的业务线动态创建业务线独立的子区块，业务线可以填充这些子区块的 DOM，公共这边提供通用的样式。创建业务线区块的时候完毕会调用 init 钩子函数，业务线可以在这个函数里做一些初始化操作。
（4）公共负责管理业务线的切换，来控制每个业务线子区块的 show 和 hide，这些细节业务线不用关心。在切入的时候会调用 onEnter 钩子函数，切出的时候会调用 onExit 钩子函数。
（5）公共会提供业务线一些公共方法调用，比如统一的 sendOrder 发单方法。还会通过事件机制和业务线通讯，比如当公共定位完成会调用 events.emit('location.suceess',posInfo) 派发事件，业务线可以监听该事件拿到定位信息。
（6）公共会提供一些封装好的通用组件，供业务线调用。
（7）业务线的 biz.js 地址是通过服务端渲染前端模板的时候通过变量传到模板里的，这个 JS 地址业务线可以自主配置，达到业务线自主上线的目的。
（8）新业务线的接入只需要提供业务线 biz.js，实现 dd.registerBiz 接口。公共不用关心具体接入的业务线，与业务线这边完全解耦。公共这边还提供了一套完整的 Wiki，方便业务线接入。

技术栈

（1）scrat 完成模块化 + 构建。

（2）zepto + gmu 实现组件化。

（3）前端模板 handlebar。

（4）combo 服务。

部分代码示例

业务线接入的 biz.js 示例如下：

dd.registerBiz({
        id: 123, 
        _tpl: {
            // …
        },
        init: function (ids) {
            // …
        },
        onEnter: function () {
            // …
        },
        onExit: function() {
            // …
        }
    });

2. 前端工程化在WebApp的实践

需求分析

（1）支持模块化开发，包括 JS 和 CSS。

（2）组件化开发。一个组件的 JS、CSS、模板放在一个目录，方便维护。

（3）多个项目按项目名称 + 版本部署，采用非覆盖式发布。

（4）允许第三方引用项目公共模块。

（5）要支持 CSS 预处理器，前端模板。

（6）与公司的 jenkis 发布平台配合，上线方便。

（7）前后端分离，前端可以独立自主上线。

解决方案

（1）使用scrat（http://scrat.io/#!/index）做前端工程化工具，完美支持上述需求分析中的前五条需求。

（2）每个项目用一个 git 的 repo 维护，然后有专门上线的2个 repo，一个存储静态资源，另一个存储页面模板。每个项目有一个shell脚本，脚本通过 scrat 编译当前项目，把编译后的结果分别 push 到上线的 repo。然后上线的 2 个 repo 关联公司的 jenkis 平台发布上线。
（3）每个项目迭代上线前修改版本号，所有静态资源都会增量发布。上线过程先全量上线静态资源，线上模板仍然指向旧的资源，不会有任何问题。然后再上线模板，先上到预发布环境让 qa 回归，回归完后再全量上线模板，完成整个上线流程。
部分代码示例


一个WebApp项目的目录结构如下：
project
  |- component_modules（生态模块）
  |- components       （工程模块）
  |- views            （非模块资源）
  |- component.json   （模块化资源描述文件）
  |- fis-conf.js      （构建工具配置文件）
  |- package.json     （项目描述文件）
  |- index.html
  |- …


一个组件的目录结构如下：
components
  |- header
    |- header.js
    |- header.styl
    |- header.tpl
    |- logo.png

按项目名称 + 版本发布的 fis-conf.js 配置规则如下：
var meta = require('./package.json');
fis.config.set('name', meta.name);
fis.config.set('version', meta.version);
// 自定义发布规则
var userRoadMap = [
    {
        reg: /^\/components\/(.*\.tpl)$/i,
        isHtmlLike: true,
        release: '/pages/c/${name}/${version}/$1'
    },
    {
        reg: /^\/pages\/(.*\.tpl)$/,
        useCache: false,
        isViews: true,
        isHtmlLike: true,
        release: '/pages/${name}/${version}/$1'
    },
    {
        reg: /^\/pages\/boot\.js$/,
        useOptimizer: false,
    },
    {
        reg: /^\/pages\/(.*\.(?:js))$/,
        useCache: false,
        isViews: true,
        url: '/${name}/${version}/$1',
        release: '/public/${name}/${version}/$1'
    },
    {
        reg: /^\/pages\/(.*\.(?:html))$/,
        useCache: false,
        useOptimizer: false,
        isViews: true,
        release: '$1'
    },
    {
        reg: /^\/pages\/(.*)$/,
        useSprite: true,
        isViews: true,
        url: '/${name}/${version}/$1',
        release: '/public/${name}/${version}/$1'
    }
];
var defaultRoadmap = fis.config.get('roadmap.path');
fis.config.set('roadmap.path', userRoadMap.concat(defaultRoadmap));

编译后部署的目录结构如下：
|-public （生成的静态资源目录）
    |- c
      |- project
        |-1.0.0
          |- header
           |- header.css
           |- header.css.js
           |- header.js
        |- home
        …
    |- project
      |- 1.0.0
      |- lib
 |- index.html
 |-views    （模板目录）
 |- …

3. 通用地图JS库的设计和实践
需求分析

（1）支持多种地图、多种地图场景的开发。

（2）屏蔽底层地图库（高德、腾讯）的接口差异。 

（3）实现小车平滑移动。
解决方案
（1）底层对腾讯地图和高德地图分别封装（不会在源码中出现 if(qq){} 风格的代码)，依据 webpack 动态打包成 2 个 JS文件，上游根据需求异步加载 JS ，对外提供同一套编程接口。
（2）抽象地图场景的概念，可以通过接口注册一个场景类，在场景中可以操作各种封装好的地图组件和方法，编写业务逻辑，实现需求。

（3）小车的平滑移动通过封装地图 SDK 提供的底层 marker，轮询小车坐标点，实现小车平滑移动（CSS3），并把“移动 + 转向 + 移动…”一系列操作抽象出动画队列的概念。

技术栈

（1）原生 JS。 

（2）webpack 打包。

行程分享实践

行程分享这个场景中，有等待接驾、行程中、行程结束等状态，有轨迹，小车平滑移动等功能。我们要做的就是利用通用地图 JS 库暴露的接口去编写行程分享的逻辑。
贴一下部分代码，看一下如何去使用封装好的地图 JS 库。

我们可以先去写一个行程分享的场景：tripShare.js
var Map = window.map;
var _ = Map.utils._;
var inherit = Map.utils.inherit;
var api = Map.utils.api;
var config = Map.utils.config;
var EventEmitter = Map.utils.EventEmitter;
var Car = Map.component.Car;
var StartPoint = Map.component.StartPoint;
var EndPoint = Map.component.EndPoint;
var TrackControl = Map.control.TrackControl;
var TrafficControl = Map.control.TrafficControl;
var TrafficLayer = Map.layer.TrafficLayer;
var Polyline = Map.Polyline;
function TripShare(map, options) {
    TripShare._super.call(this);
    // …
}
inherit(TripShare, EventEmitter);
TripShare.prototype.begin = function () {
    // …
};
// …

然后我们这样去注册场景。
var Map = window.map;
var fromlat = 31.17626;
var fromlng = 121.425;
var tolat = 31.20425;
var tolng = 121.40398;
Map.ready(function (mapInstance) {
    var map = mapInstance.createMap('container', {});
    var TripShare = require('./tripShare');
    var scene = map.scene.register(TripShare, {
        orderStatus: 1,
        url: 'xxxx',
        oid: 'aaaa',
        pathUrl: 'xxxx'
        fromlat: fromlat,
        fromlng: fromlng,
        tolat: tolat,
        tolng: tolng,
        usePath: true
    });
    scene.begin();
    scene.on('path.badCase', function(badCase) {
        // do anything
    });
});


我们可以调用场景的方法，又由于场景继承了 EventEmitter 事件中心，它会通过 trigger 派发事件，我们可以监听这些事件，去做一些事情。


4. 统一登录SDK的设计
需求分析

（1）滴滴有众多业务线，每个业务线都有独立的域名，需要打通各个WebApp域名的登录态。

（2）方便新老业务线、运营活动等页面接入登录。

（3）提供简单、友好的接口。
解决方案

（1）与账号部门合作，通过跨域方式访问 passport 域名下的接口。跨域方案是通过 iframe passport 域名下的页面，利用 postmessage 进行通信。登录成功后会在 passport 域名下利用种下 ticket。后端提供判断是否登录的接口，前端请求这个接口的时候会从 passport 域名下读取 ticket 并把它作为请求的参数传给后端，这样一旦用户在 a 域名下登录成功，那么在 b 域名下调用是否登录接口，返回的就是登录成功的结果，这样就打通了多个域名的登录态。
（2）封装复杂的登录交互细节，对外提供简单的交互接口。
（3）提供完善 Wiki 文档，建立专门的钉钉服务交流群。

技术方案

henimages1

技术栈

（1）原生 JS。

（2）webpack 打包。
5. 通用客户端JSBridge的封装

需求分析

（1）内嵌在滴滴 App 端里的页面，需要通过 JSBrigde 的方式获取端的一些能力。 

（2）屏蔽 iOS 端和 Android 端的一些底层通讯差异。 

（3）提供简单、友好的接口。

解决方案
（2）对端的一些具象接口，比如分享微信、分享微博等做更高级封装，提供share接口，通过参数指定分享到不同的渠道。
（3）提供完善 Wiki 文档，建立专门的钉钉服务交流群。

技术栈

（1）ES6 + eslint。 

（2）webpack 打包。





````````````````````````````````````````````````````



部分代码示例：

```
export function initGlobalAPI(DDBridge) {
    each(config.api, (conf, name) => {
        DDBridge[name] = makeBridgeFn(conf);
        DDBridge[name].support = conf.support;
    });
    initSupport(DDBridge);
    initVersion(DDBridge);
    initShare(DDBridge);
    initPay(DDBridge);
};
export function makeBridgeFn(conf) {
    return function (param = '', callback = noop) {
        if (arguments.length === 1 && isFn(param)) {
            callback = param;
            param = '';
        }
        let fn = conf.fn;
        if (supportPrompt) {
            promptSend(fn, param, callback);
        } else {
            bridgeReady((bridge) => {
                bridge.callHandler(fn, param, (data) => {
                    if (isStr(data)) {
                        data = JSON.parse(data);
                    }
                    callback(data);
                });
            });
        }
    };
};
```

6.在公共部门做通用服务的一些感悟

入职滴滴一年，造了不少公司级别的“轮子”，不少轮子已经在业务线跑起来了，运行状况还算可以。我也总结了做通用服务要注意的几点。

（1）一定要好用，用起来要简单。

这是我一直贯彻的理念，如果通用服务不好用，那一定会受到质疑和吐槽。同样我们用开源的框架，也一定会选简单好用的，当年 jQuery，prototype，tangram 等 JS 库百家争鸣的时候，jQuery笑到了最后，为什么呢？很简单：jQuery好用啊，一个 $(xxx) 搞定一切。相比 tangram 那种 Baidu.T.createDom() 的方式，高下立判。

我们在设计通用 JS 库的时候，一定要站在更高的角度去对需求做抽象。比如在设计统一登录 SDK，首先要想的不是复杂的交互逻辑、如何去实现、有哪些技术难点，而是去想，别人怎么用这个库，怎么用起来爽。登录的需求就是用户触发一个登录动作，登录完成能拿到用户一些信息，所以我就设计一个login(callback)接口，那么使用方只需要简单调用这个方法，就可以完成登录需求，而不用去关心登录各种复杂的细节。

（2）该做封装的地方要封装，对外暴露的接口越少越好。

封装很重要，举个通俗的例子，有一天我去洗手，发现水龙头的开关把手没了，把原始的开关暴露给我了，虽然也能用，但是体验就会很不好。水龙头的开关把手就是对原始开关的封装。我在做 JSBridge 库 的时候，也是一样的道理，如果让用户直接调用 iOS 和 Andrid 提供的原生 bridge 接口的，也能 work，但是非常难用，需要判断 iOS 和 Android 接口的差异，还需要考虑 bridge ready 事件后才能执行方法等，这些都是我原本不需要关心的细节。所以我们的库就是帮助用户封装掉这些“脏活”，对外提供简单的 DDBridge.funcName(options,callback) 接口，优化使用体验。

为什么说对外暴露的接口越少越好，因为接口越多，则说明用户的学习成本越高，比如如火如荼的 Vue.js，其1.x 版本很多接口的功能大同小异，所以在 2.0 版本的 Vue 就干掉了很多接口，减少了用户的学习成本。同样的，我们在做 JSBridge 分享接口相关的时候，也通过一个share接口封装了端提供的微信分享、支付宝分享、微博分享等接口。

（3）先思考再动手，设计合理的代码组织方式。

在写代码之前，一定要先思考清楚，切忌上来就写代码，那样很容易写成一波流代码。合理的代码组织方式，有利于代码的扩展和维护，最基本的就是模块化。这里没有银弹，需要大量的实践和总结，学会抽象的看问题，看一些设计模式相关多书籍，多看优秀的开源的代码，可以先从模仿开始。

由于我们写的是通用服务，用户也可能会提出各种需求，当遇到这个问题的时候，不能上来就写代码去实现甚至hack，而是先思考这个需求是不是可以抽象成通用的需求，如果不能抽象，我们如何更优雅的实现，之前的设计是不是有问题。总之，要多想多思考，也可以和小伙伴讨论，争取做到是在设计代码而不是堆代码。

（4）追求体验极致。

现在很多前端都在玩 Node，玩构建工具，玩 MVVM 框架，玩 ES6，好像感觉学会了这些就可以提高身价。其实，这些大部分都是工具，是服务我们平时工作的，不要忘了我们的本行还是前端，还是需要写页面的。其实前端有些组件和效果如果想要追求体验极致的话，也不容易。如果能做到极致，身价也不会低。举个例子，我在写 mofang 移动端组件的时候，有个筛选器组件 picker，类似 iOS 原生 UIPickerView 的东东，我当时拿到需求的时候，也从 GitHub 上搜索过，没有满意的，体验都很一般，于是我就对比 iOS 原生的 UIPickerView的体验，思考它的实现、一点点细节的调试，最终也撸出来体验几乎一致的移动端 H5 picker 组件。举这个例子其实想说明，我们在做通用服务的时候，要多花心思，如果能做出一些极致体验的东东，不仅对用户来说他们很乐意使用，对自己也是一种锻炼。

（5）一定要写 Wiki。

要写 Wiki！要写 Wiki!要写 Wiki！重要的事情说 3 遍。由于我们做通用服务，免不了和用户打交道，Wiki 就尤为重要了。我们需要把通用服务的接口，使用方式，常见问题等都写清楚。好的文档可以很好的指导用户如何使用我们的服务，这样可以大大的减少沟通成本，节约我们自身和用户的时间。

（6）要学会销售。

有些人可能会觉得写通用服务似乎比做业务的同学更高大上，其实不然，本质上我们都是在为公司打工，都是在输出自己的价值，只是做事的重心不同。那么做公共的同学的价值在哪里？就是让自己写的通用服务被更多的人用，去提升他们的工作效率。所以，我们要学会销售自己的服务，而不是写完一个的服务摆出一副你爱用不用的态度。如果你写出来的东西没人用，就算它再牛逼，对公司的价值也是 0。另外，我们还要学会从业务中去沉淀服务，要去发现业务中的痛点，可以提升效率的地方，然后用技术的手段和工具去解决它。

（7）一颗服务的心。

做公共的同学一定要有颗服务的心。我们售卖的是自己的服务，那么也一定要做好售后服务，除了 Wiki，各种沟通钉钉微信沟通群也要积极响应，耐心的去帮助用户解决问题，其实很多时候，都是靠着用户去帮我们去发现 Bug ，完善功能和优化体验的。

7.个人成长

我入前端这行已经4年了，在学校的时候我是玩 .net 的，喜欢折腾。毕业后当然和大部分应届生一样，渴望进 BAT 这样的大公司，不过 BAT 几乎不招 .net 的岗位。由于我读研的时候做过一些网站方向的开发，所以就投了百度的一个相近的职位——Web前端开发。这里我要特别感谢我百度的mentor张袁炜，他是一个对技术要求很高的人，受他的影响，我也成为一个对技术有追求的人。四年来，我写过页面，写过网页游戏、写过Chrome插件、写过框架、写过组件、写过服务，由于一直在做不同的东西，每一年我都有所收获。

兴趣导向，有的时候我感觉写代码和玩游戏是一样爽的事情，我也很喜欢看优秀的开源作品，看看他们的代码设计、技术细节，会吸收一些不错的东西到自己平时的工作中。

前端这几年发展很快，新技术层出不穷，有的时候，我们要跳出自己的舒适圈，接纳一些新事物，新技术，去让自己不断学习，而不是满足于自己已掌握的那些技术。这里我不是去倡导滥用新技术，而是要保持一颗学习的心态，一颗包容的心态。

感谢今天的精彩分享，现在是30分钟的提问和交流时间。提问时，请将自己的问题编号并附上前缀“B问题”，如：B问题8：xxxx，注意，不符合格式的，问题一次性描述不清楚的，追问的，嘉宾可以不回答。





B问题1：面对层出不穷的框架和工具库，我们该如何选择？
1.要选择适合自己业务需求的框架，这个“合适”是一定是需要有经验的架构师或者高工做技术选型。
2.一些基本场景参考，比如做PC内部MIS系统可以选择Angular和React，移动端可以选择Vue等。
3.要看这个框架or工具是否足够“靠谱”：是否有人维护，issue是否能及时响应，和周边社区和生态工具是否完善。
4.关于我们，公共团队相对业务团队一定是跑的更快的，在不断的调研试错，内部培训+评审，有了解决方案就大胆实践。

B问题2:组件的版本控制有什么手段
比如用webpack构建的时候，可以在output输出的时候在目录结构上加入版本号，版本号可以读取package.json文件中的版本号。举个例子，可以这样配置：
```
var version = require('../package.json').version;
var name = config.build.mofangModuleName;
var vname = version + '/' + name;

var webpackConfig = merge(baseWebpackConfig,)
	entry: './src/index.js',
	output: {
		path: config.build.mofangPath,
		filename: vname + '.min.js',
		library: name,
		libraryTarget: 'umd',
	},
```

B问题3: 开发移动端如何选择使用原生iOS开发还是html5开发?
这个问题有点大，原生开发和h5开发其实各有所长，主要还是看场景。原生的优势可能在于一些对性能要求高的场景，比如游戏，体验会更好。H5开发在于一些频繁迭代的页面，h5上线简单，没有发版的压力。H5还有一点优势，可以减少包体积，h5和原生混合的应用场景的趋势约来越多。

B问题4:前端组件化开发与管理，是怎样进行跨模块调用的，以及后期维护的方式?
1.跨模块这个概念有点模糊，如果是组件依赖一些公共资源，我们一般会和components平级放一个common目录，这个目录里会有一些通用的JS、CSS、图片等公共资源。如果是指组件之前的通讯，那么如果是父子组件的通讯，一般来说父组件会依赖子组件，它能够调用子组件的方法。而子组件是不依赖父组件，它是可以放在任何地方，可以通过事件的派发通知父组件，但不能主动调用父组件的方法；如果是平级组件，可以通过全局事件中心去做通讯。2.组件的维护肯定是把组件依赖的js、css、模板、图片放在一个目录就近管理。

B问题5，随着业务复杂性递增，单元测试是否同步跟进。UI层面是否部署自动化测试。开发人员是否需要编写测试代码?
这是个好问题，单元测试确实很重要，现在一些流行的MVVM框架比如Vue，都提供了很好的单元测试。UI部署自动化测试确实也很重要，这一块滴滴这边做的也还不够，做了一小部分的尝试，大部分页面还都是在黑盒测试。开发人员如果业务压力不是特别大的时候，编写一些测试代码是很好的习惯，可以基于现在一些流行的测试框架写，是值得提倡的做法。

B问题6，对于小公司，只有一个前端，没有架构师，对于技术选型和单元测试等相关，我们该怎么办？
1. 可以多关注一些业内的比较热和新的技术，然后看看他们的应用场景，有没有和自己业务比较贴合的点。
2. 可以加一些类似“前端之巅”这样的技术讨论群，和一些厉害的或者有类似经验的人交流。不过要注意提问题的方式，问题首先是要自己经过思考的，其次是把问题具象化，不要问太大的问题。
3.有的时候，对于创业公司而言，可能快是最重要的，所以做技术选型的时候也可以规避掉一些学习成本高的框架，选一些能快速上手开发业务的。
4. 最关键的一点，还是要不断自我学习，提升自我的能力。在做业务的时候多思考，看看流程中哪些不合理的地方，可以提升效率的地方，有没有好的技术和工具去帮你解决和提升效率。把大问题简化拆分成一个个小问题，一点点的优化。

B问题7，对于展示性，交互比较多，数据量少的活动，专题类页面，怎么快速开发，进行组件化开发？
1. 对于h5专题运营活动类的开发，短期可以基于一些比较流行的h5开发框架开发，过程中可以做抽象，把一些通用的功能封装，模块化，组件化，未来可以复用。
2. 长期来说可以做一套h5编辑器，提供若干套模板和若干种组件，通过配置化或者可视化编辑的方式，让运营同学自己编辑生成一个运营活动页面。
3. 我们公共这边还整理了一套动画案例库，对于复杂的动画做收录，便于以后的参考和复用。

A问题1：滴滴的构建工具用的是FIS吗？
恩，滴滴公共团队这边的Webapp项目是基于scrat做构建的，它是在FIS基础上二次开发的产物。公共这边的一些基础组件库，是基于webpack打包的。

A问题2:公共团队在支持业务团队方面（问题咨询、排错等），有什么好的经验分享？
1.首先要有wiki和demo。
2.会建一个钉钉群和一个微信群，把需要咨询问题的同学和相关技术产品同学拉到一起，常规问题都会在群里解决。3.也会定期组织内部分享，和业务的同学一起聊聊，问问他们在做什么，有什么痛点，也告诉他们我们做了什么，有什么可以用的。4.服务意识很重要。当业务同学出现紧急情况比如上线依赖公共的一个服务出现问题，一定会安排人力第一时间支持和解决，不管是加班甚至熬夜（当然不是常态），会让他们对公共产生安全感和信任。

A问题3:能否介绍下你平常一般怎么学习前端技术的 看书？还是找技术网站 或者只在github上看？
1.看书。系统的学习是很重要的，沉下心来把书中的技术点掌握，一定会比只在网上看一些快餐类的文章效果好。而且出来前端语言方面的书籍，一些周边的书籍比如《HTTP权威指南》、《设计模式》、《精通正则表达式》等等不错的书都可以好好研读。当然，关注一些Weekly也是很好的习惯。
2.兴趣导向。我很喜欢编程，所以平时也会多敲代码，除了工作之外，我会花自己的业余时间学习。可以找一些自己的兴趣点，比如对h5游戏感兴趣，我就自己写了几个小游戏如2048，连连看。比如连连看我想做多人对战，就又顺便学习了socket.io。
3.github上看优秀的开源代码，这里是要有选择性的看，因为毕竟时间经历有限。举个例子，比如我最近在用Vue框架，我会想一下她的数据视图绑定原理是怎么实现的，这样带着问题去看。看之前我会先看它的官网、文档和一些周边文章。对他的功能和设计大概了解了以后，再去看实现的细节。看源码的过程中看到一些不错的设计的代码吸收过来。