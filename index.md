---
layout: page
title: 西红那个柿
tagline: 记录点滴前端知识
---
{% include JB/setup %}





### 前端工程

0. 开发流程工程化：[FIS](http://fis.baidu.com)的思路，解决本地开发、调试、编译、部署、性能优化自动化等问题
    * 模块化框架
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
2. [整站JS错误监控](http://blog.newrelic.com/2014/03/13/javascript-error-reporting-ajax-timing-new-relic)：整站部署JS脚本错误监控，并且有报警机制（在指定的时间段内报错数量达到限制数量）， ![](http://gtms02.alicdn.com/tps/i2/TB1KJGJGXXXXXbUapXXXGNj1FXX-1286-697.jpg)
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
4. Webapp、Hybird跟Native的webview如何互相结合：Hybird API的方式来做，API的定义参考HTML5的W3C定义，一方面可以面向未来，而来可以很好的兼容第三方browser的支持
    * 借助于Native可以获取到系统更多的API支持，并且下发给webapp页面使用
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
1. 前后端分离方案：
    * 纯前端的页面渲染方案：MVC、MVVM等等，[Vue.js](http://vuejs.org/)、[Angularjs](http://angularjs.org/)、[Backbonejs](http://backbonejs.org/)等等
    * 服务端页面渲染：本地集成开发工具。
    * 本地开发、数据模拟、自动化测试、提交测试、发布上线等整个开发流水线的工程
  
  
  
### 技术点整理

0. [HTML Imports](http://www.html5rocks.com/zh/tutorials/webcomponents/imports/)：真正意义上的一个完整的前端模块：HTML、CSS、JS都在一起了，而且JS也不用根据传统的方式去动态加载CSS，将HTML模板写在JS中了，一个模块就是一个document，还是互相独立的引用，互相不耦合。
    * 将相关的HTML/CSS/JS 作为一个单独的包 来分发
    * 代码组织：更加模块化，表现、结构、逻辑分离
    * 并行HTML解析：这是首次能够让浏览器并行运行两个(或多个)HTML解析器
0. [Web Component自定义标签的应用](http://developer.telerik.com/featured/web-components-ready-production)：自定义标签，已经在高级浏览器得到了支持，并且能够很好的自定义一个标签，并且给标签做初始化处理，通过自定义标签，可以很方便的实现一些纯JS的模块化的功能。
1. [dragula](https://github.com/bevacqua/dragula) Drag and drop so simple it hurts 
[http://bevacqua.github.io/dragula](http://bevacqua.github.io/dragula)，Browser support includes every sane browser and IE7+.
0. [The Great Web Module Compendium](http://ponyfoo.com/articles/great-web-module-compendium)