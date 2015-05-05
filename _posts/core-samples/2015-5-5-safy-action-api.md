---
layout: post
category : lessons
tagline: ""
---
{% include JB/setup %}

Safy作为一个前端自动化测试平台，监控页面的交互行为是重中之重，为此，创建了下面的用户行为相关的API：

{% capture text %}
/* Tip：凡是涉及到传递目标元素参数的，都支持selector或者DOM元素的引用的方式 */
 
/* 创建一个行为（一个case里面可以声明多个行为）*/
var action = monitor.createAction();
//可以带个参数，指定初始目标元素
var action = monitor.createAction({
    target : "#txt"
});
 
//目前Action下的方法有：scroll/keydown/type/click/clickOnce/mouseover/mouseup/mousedown/wait/complete/end，scroll、keydown、type、click、mouseover、wait方法支持链式调用
// scroll: 滚动页面的滚动条
// keydown: 对输入的input/textarea触发keydown事件
// type: 对一个输入框(input,textarea,select) 赋值
// click: 触发一个元素的click操作(会使用三种方式去触发：原生的fireEvent、jQuery trigger、调用元素的click方法)
// clickOnce : 触发一个元素的click操作（只使用一种方法触发事件：原生的fireEvent）
// mouseover : 触发一个元素的mouseover操作
// mouseup : 触发一个元素的mouseup操作
// mousedown : 触发一个元素的mousedown操作
// wait: 等待多长时间继续执行下一个步骤
// complete/end: 显示调用该行为结束，并且设置该单侧已完成（如果有多个行为，则最后一个行为调用complete/end方法即可，如果只有一个，那么该行为调用complete/end以结束该单侧）
 
 
/*
 * 特别说明一下click/clickOnce的存在目的：有些场景去触发click事件，使用上面三种方法中的某一种都没法触发，
 * 所以结合三种情况去触发，
 * 但是这样的话，有可能事件会被触发三次，或者被触发一次，其他的触发无效，这是为了保证click一定会被触发。
 * clickOnce就是为了上面的被触发多次后本身出现问题，所以它就是用原生的fireEvent去触发一次。
 */
 
 
/* 开始执行行为 */
action.type("123456");
//或者指定目标元素
action.type("#txt","123456");
//or
action.type(document.getElementById("txt"),"123456").complete();
//or
action.type("123456",function(el){
    console.log(el.value);
}).complete();
 
//滚动条：滚动到300的位置
action.scroll("300",function(){});
 
//keydown事件，需要按键的keyCode
action.keydown("#example","8",function(el){});
 
//带点击行为（mouseover行为类似）
action.type("#txt","12345").click().complete();
//带一个回调，回调函数的参数就是目标元素的DOM引用
action.type("#txt","123").wait(1000).click(function(el){
    console.log(el.value);
}).complete();
 
//在行为中也可以重新指定目标元素
action.type("123").wait(2000).click("#btn",function(el){}).complete();
 
//其实，wait/end方法也是有回调函数的，可以用在一些点击按钮发送jsonp的场景里面，验证效果
action.type("#txt","123").wait(2000).click("#btn").wait(2000,function(){
    console.log($("#txt").val());
});
 
//录制出来的代码如下所示：
var action = monitor.createAction();
.type("#op_hangban_start","s",function(el){})
.wait(654,function(){})
.click("#tangram-suggestion--TANGRAM__3-item5",function(el){})
.wait(2248,function(){})
.type("#op_hangban_end","s",function(el){})
.wait(639,function(){})
.click("#tangram-suggestion--TANGRAM__g-item7",function(el){})
.complete(function(){});
{% endcapture %}

这套用户行为API简单明了，不管FE/QA都能很快的上手去编写测试单侧。

如果嫌手动创建用户行为的单侧代码不方便，那么还会有更方面的是Safy提供了录制页面行为的工具，然后直接把行为转化为上面的API单侧代码，直接可以运行，可以做到对于简单的交互行为，FE/QA零成本的创建一个单侧用例。

