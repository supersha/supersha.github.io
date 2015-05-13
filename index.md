---
layout: page
title: 西红那个柿
tagline: 记录自己的前端生涯
---
{% include JB/setup %}


### 思考和总结

0. 前端工程化：[FIS](http://fis.baidu.com)的思路，解决本地开发、调试、编译、部署、性能优化自动化等问题
    * 模块化框架：requirejs、seajs、modjs...
    * 模板：后端模板、前端模板
        * 后端模板：可采用PHP Smarty来做，LAMP容易搭建并且有成熟的工具
        * 前端模板：可以开发一个模板，并且支持转成其他模板的语法：编写一种模板，可以转成Smarty等模板语法，**开发一套模板，前后端都可使用**
    * 调试工具
    * 性能优化自动化
    * 部署方案：需要前后端，并且运维的支持合作
1. 对于webapp、hybird应用的开发，调试工具非常重要，需要一个很好的工具来支持在手机上看效果、PC上调试，提高开发效率
1. 整站性能监控：整站部署性能采集脚本，然后通过url作为key的方式，整合性能数据，图表展示，并且制定一个**性能标准**，根据性能标准来做报警机制（邮件、短信、IM即时通讯工具提醒等），并且有日常报表发送功能
    * 对于webapp、hybird应用尤其重要，需要对发布的页面进行性能检测（真机性能测试、可以模拟平均网速：wifi、3g、2g环境的情况）
    * 对于以图片为主的业务，对图片的压缩尤其重要，可以CDN自动压缩机制，对于页面的sprites图，通过工具在开发编译阶段做好压缩和优化
2. [整站JS错误监控](http://blog.newrelic.com/2014/03/13/javascript-error-reporting-ajax-timing-new-relic)：整站部署JS脚本错误监控，并且有报警机制（在指定的时间段内报错数量达到限制数量）
    * window.onerror方案：如果要支持获取到脚本出错的详细信息：error message, stack trace, browser version, user agent string, url，一般静态资源都会CDN化，跟主页面的域名不同域，所以需要js的CDN支持跨域的响应头CORS的设置，只设置针对自己站点的支持即可，该方案简便，多终端支持。
    * 常规的自动化监控webdriver、phantomjs、slimerjs模拟手持设备：可以从底层拿到错误的详细信息
    * Ajax请求的监控：响应的状态码、响应错误、响应的时间分布等数据
3. 整站操作系统、浏览器、版本分布等数据：可以实时了解到整张的运行设备的情况并做出响应的决策
4. PV、UV等流量监控系统
5. 页面用户行为数据采集、分析、报表系统
3. 常规的线上自动化监控：平台化的思路，提供测试代码的集成、报警、报表机制
    0. 请求404
    0. 代码扫描：HTML、CSS、JS...
    0. 性能检查
    0. 带有业务特点的自动化检测
4. Webapp、Hybird跟Native的webview如何互相结合：
    * Hybird：API的定义参考HTML5的W3C定义，一方面可以面向未来，而来可以很好的兼容第三方browser的支持。借助于Native可以获取到系统更多的API支持，并且下发给webapp页面使用
    * [React Native](https://facebook.github.io/react-native/)：facebook最近开源的项目
5. 拥有一套可以灵活的整站部署脚本的机制：目的是可以对一些整站的监控以及获取日志数据能够快速的实施并且拿到结果
    * 可以在网络层做，在响应请求的时候，直接修改响应的内容，插入全局的内容。这种方案是整站性质的，数据量会很大，需要做好抽样率的控制
    * 在模板中做，整站的页面继承于一个通用的base模板，在该base模板里面做这套逻辑。不过这个方案可能细化到业务级别。
    * 这是一把双刃剑，需要把握好，权限严格控制，发布审批等流程必须要有
0. 多终端的方案：
    * URL访问一致性。自动适配终端，做不同的展现
        * 一套模板多端自适应展现
        * 多套模板对应多个终端，需要后端有识别设备的服务，然后渲染相应的模板
    * 前端技术架构的一致性。包括基础库、框架、组件开发方式、模板、模块化方式等等，解决组件可以自适应多端展现的支持，并且使得团队的开发模式一致
    * 设备识别服务。在网络入口层做一个通用的设备识别服务，获取到设备信息，然后下发到后面的各个后端服务，这个识别服务要保持独立性和扩展性，并且要具有收集未知设备的UA信息，供离线分析，然后扩展。
0. 统一风格的UI交互、视觉规范，并实现一套UI框架。提高用户体验，以及UED、前端等的开发效率
    * 前端组件的开发、调试、多人协作、规范、使用、升级等一整套方案
1. 前后端分离方案：本地开发、数据模拟、自动化测试、提交测试、发布上线等整个开发流水线的工程
    * 纯前端的页面渲染方案：MVC、MVVM等等，[Vue.js](http://vuejs.org/)、[Angularjs](http://angularjs.org/)、[Backbonejs](http://backbonejs.org/)、[Reactjs](https://facebook.github.io/react/)等等，下面说一下我在项目中所实践的一个方案：
        * 自己造了个简单的轮子([mvm-simple](https://github.com/supersha/mvvm-simple))，单向的数据和View绑定，并且保持了比较好的JS、HTML、CSS三层分离（在HTML中即做模板，又做功能性的绑定声明的，太那个讨厌了）
        * 项目目录规范：![](http://gtms01.alicdn.com/tps/i1/TB1ejHAHpXXXXXGaXXXfUQMIVXX-993-406.png) 
        * 模块开发示意图：![](http://gtms04.alicdn.com/tps/i4/TB1PSUtHpXXXXbpaXXXHmZl1VXX-642-517.png)
        * 使用了内部一个集成开发工具（核心使用FIS，进行了一些包装，满足业务特点的需要），以及需要[juicer](http://juicer.name)模板
    * 服务端页面渲染：本地集成开发工具。
0. 接口维护的平台
    * 这个对于前后端分离之后来说，非常重要，说白了就是前端模拟数据的一部分，但是它的意义不在于模拟数据
    * 目前已有的：天猫的IF、淘宝的DIP、阿里妈妈的[RAP](https://github.com/thx/RAP)、百度也有一个（未开源）
    * 几个方面：
        0. 前端通过接口平台制定一个API接口，然后编辑该接口的JSON格式以及每一个字段的数据类型
        0. 通过该API接口，可以自动随机生成一个JSON模拟数据，然后可以给到前端渲染页面，而不依赖后端的数据
        0. 也可以生成一个规范的JSON Schema，然后给到测试同学，对接口进行自动化测试和校验
    * 最大的意义在于：这样的一个接口平台比死的接口文档来的更好维护，在项目后期的日常维护中特别有帮助，可以让多个角色（测试、后端等）都可以很方面的维护和编辑，然后前端就可以自动拿到模拟的数据。保持了这个API接口约定的可维护性。
  
<br>

### 技术点整理

0. [HTML Imports](http://www.html5rocks.com/zh/tutorials/webcomponents/imports/)：真正意义上的一个完整的前端模块：HTML、CSS、JS都在一起了，而且JS也不用根据传统的方式去动态加载CSS，将HTML模板写在JS中了，一个模块就是一个document，还是互相独立的引用，互相不耦合。
    * 将相关的HTML/CSS/JS 作为一个单独的包 来分发
    * 代码组织：更加模块化，表现、结构、逻辑分离
    * 并行HTML解析：这是首次能够让浏览器并行运行两个(或多个)HTML解析器
0. [Web Component自定义标签的应用](http://developer.telerik.com/featured/web-components-ready-production)：自定义标签，已经在高级浏览器得到了支持，并且能够很好的自定义一个标签，并且给标签做初始化处理，通过自定义标签，可以很方便的实现一些纯JS的模块化的功能。
0. [The Great Web Module Compendium](http://ponyfoo.com/articles/great-web-module-compendium)
0. -webkit-overflow-scrolling:touch iOS7+可以很好的支持滚动的流畅性，overflow hidden之后不再生硬
0. iOS8+ 已支持0.5px的border声明，让border更接近Native

<br>

### 一些有意思的Project

0. [jterrace / js.js](https://github.com/jterrace/js.js/) A JavaScript JavaScript interpreter
0. [Every javascript project you should be looking into](http://www.javascriptoo.com/)
0. [Effeckt.css](http://h5bp.github.io/Effeckt.css/)
0. [josh / css-explain](https://github.com/josh/css-explain) SQL EXPLAIN for CSS selectors
0. [blueimp / JavaScript-MD5](https://github.com/blueimp/JavaScript-MD5) JavaScript MD5 implementation. Compatible with server-side environments like node.js, module loaders like RequireJS and all web browsers.
0. [dan-silver / ElementTransitions.js](https://github.com/dan-silver/ElementTransitions.js/) Simple transitions for web pages
0. [fex-team / yog2](https://github.com/fex-team/yog2) 基于 express 支持前后一体化开发的框架
0. [thingsinjars / cssert](https://github.com/thingsinjars/cssert) CSS verification testing，特色就是“页面录制工具+自动生成它所能解析的数据接口”，然后去重现这些样式，看是否跟录制的对的上号
0. [dragula](https://github.com/bevacqua/dragula) Drag and drop so simple it hurts 
[http://bevacqua.github.io/dragula](http://bevacqua.github.io/dragula)，Browser support includes every sane browser and IE7+.
0. [victorquinn / chancejs](https://github.com/victorquinn/chancejs) Chance - Random generator helper for JavaScript，生成一个随机字符串
0. [philipwalton / html-inspector](https://github.com/philipwalton/html-inspector) HTML Inspector is a code quality tool to help you and your team write better markup
0. [CSS3 Arrow](http://cssarrowplease.com/) CSS3实现的一个arrow，挺方便的
0. [jsonnet](http://google.github.io/jsonnet/doc/userdocs.html) Google开源的一个扩展JSON能力的项目，使得JSON有了语法的概念
0. [facebook / immutable-js](https://github.com/facebook/immutable-js) Immutable persistent data collections for Javascript which increase efficiency and simplicity.
0. [ftlabs / fastclick](https://github.com/ftlabs/fastclick) Polyfill to remove click delays on browsers with touch UIs. 解决click事件300ms延迟的问题，zepto也有类似的tap事件的实现方案
0. [hammerjs / hammer.js](https://github.com/hammerjs/hammer.js) [http://hammerjs.github.io/](http://hammerjs.github.io/) 轻量级的Touch/Gesture手势库
0. [muut / riotjs](https://github.com/muut/riotjs) [https://muut.com/riotjs/](https://muut.com/riotjs/) 类似于Reactjs的一个轻量级库，在模块方面，将JS+Template+CSS整合到一个文件中来维护和编写，保持了模块的独立性和维护性，挺不错的一个方案，由于轻量级，在手机端可以更好的尝试下。
0. [Vue.js](http://cn.vuejs.org/) 轻量级的MVVM，算是Angular的精简版。提供了模板引擎+事件绑定+DOM自动操作，在手机端也还是一个不错的选择
0. [richtr / NoSleep.js](https://github.com/richtr/NoSleep.js) Prevent display sleep and enable wake lock in any Android or iOS web browser。在浏览器端就可以控制手机屏幕是否进入待机状态，挺有意思的一个hack技巧
0. [krasimir / lsbridge](https://github.com/krasimir/lsbridge) Using local storage as a communication channel

<br>

### 自己做过/写过的一些东西

* [frontend.duapp.com](http://frontend.duapp.com) 为前端开发人员提供最新的前端技术文章，囊括国内外知名博客、站点等技术文章。
* [mvm-simple](https://github.com/supersha/mvvm-simple) 单向的数据和View绑定，并且保持了比较好的JS、HTML、CSS三层分离
* 支持Expires过期时间的localStorage对象封装：[supersha / storage.js](https://github.com/supersha/storage.js)，Usage：[supersha / 5902372](https://gist.github.com/5902372)
* [Safy](https://github.com/supersha/safy) 纯前端自动化测试系统（在百度期间的命名是Safy）
    * [Safy平台中使用到的用户行为API](/lessons/2015/05/05/safy-action-api/)
    * [ACE在线编辑器的AutoComplete功能](https://gist.github.com/5230745) 给ACE写的一个AutoComplete扩展功能，方便写代码。[界面截图](http://bcs.duapp.com/diandiblog/QQ20130624-1.png)
    * [获取指定DOM元素的Selector](https://github.com/supersha/safy/blob/master/static/js/get_selector.js)
    * [Safy中的should.js](https://gist.github.com/5932377)
* 猫须（在天猫期间，Safy更名为猫须）
    * [平台规划图](http://gtms03.alicdn.com/tps/i3/T1557bFbVfXXaA3NTU-1264-685.png)
    * [运行服务架构图](http://gtms04.alicdn.com/tps/i4/TB1DBpNHFXXXXXUapXXjSpJVFXX-597-475.png)
    * [运行任务代码逻辑示意图](http://gtms03.alicdn.com/tps/i3/TB16L0zHFXXXXbJaXXX9tEjOVXX-583-684.png)
    * [用例的运行方式](http://gtms02.alicdn.com/tps/i2/TB1c3ueHFXXXXXBapXXuFqpYpXX-633-377.png)
    * 猫须的思想
        * 任务+用例的模式
            * 用例，是猫须里面所定义的最小的单元，在用例中，可以是一个通用的测试单元，比如：检测JS文件编码，也可以是业务功能测试的封装，比如：检查搜索链接入参合法性，然后就可以在“创建任务”的时候，勾选这些自己创建的用例。
            * 用例有“公有”和“私有”之分，其实也就是是否想把自己创建的用例提供给其他人使用
            * 任务，是猫须里面目前最大的单元，错误报表等目前都是以任务为纬度来发送的，目前猫须这么设置，还是有问题的，应该以“项目”为最大的纬度，一个项目下面包含了任务，任务包含了各种用例模块。这个会在接下来的规划中来实现。 ![](http://gtms03.alicdn.com/tps/i3/TB1Jh2OHpXXXXcbaXXXG0YeVFXX-493-211.png)
        * 平台跟运行服务相分离：平台是GUI的用例和任务管理平台，运行服务是运行任务，保持两者的分离，方便独立部署和扩展。
        * 创建任务的多样性：![](http://gtms01.alicdn.com/tps/i1/TB1gb1sHFXXXXXdapXXHHaWIFXX-808-203.png)
* 性能优化随想。比较喜欢从一个点开始出发，开始发散，联想到更多的前端更多的东西。 [思维导图](http://bcs.duapp.com/diandiblog/%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96.png)
* [玩了玩iOS设备的螺旋仪](https://gist.github.com/5918279) CSS3里面的transform可以做图形变换的效果，它有2D和3D的效果，rotate有rotateX, rotateY, rotateZ三个方向上的变换，根据要实现的效果就使用rotateY来做左右的倾斜变换的效果。从DeviceOrientationEvent事件属性中获取到gamma属性，也就是左右上下方向的倾斜度，然后把这个属性的值动态写到transform中
* [page chekcker](https://gist.github.com/6007327) 检查页面不符合最佳实践的方面
* [console.duapp.com](http://console.duapp.com) 用于自己在内部开发中使用，调试移动端的页面功能 [界面截图](http://bcs.duapp.com/diandiblog/QQ20130625-1.png)
* 使用PHP做过一个Combo服务，服务端合并多个js文件并设置相关的缓存
* 折腾了多个本地集成开发环境平台（根据不同的业务场景），前后端分离相关项目的基础建设
