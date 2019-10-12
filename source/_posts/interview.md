---
title: 前端面试问题总结一
date: 2019-09-17 15:38:10
tags:
    - 面试
    - 前端
---
## 一、本地存储
在较高版本的浏览器中，js提供了sessionStorage和globalStorage。在HTML5中提供了localStorage来取代globalStorage。
html5中的Web Storage包括了两种存储方式：sessionStorage和localStorage。
sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。
而localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。
<!-- more -->
### web storage和cookie的区别
Web Storage的概念和cookie相似，区别是它是为了更大容量存储设计的。Cookie的大小是受限的，并且每次你请求一个新的页面的时候Cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可以跨域调用。
除此之外，Web Storage拥有setItem,getItem,removeItem,clear等方法，不像cookie需要前端开发者自己封装setCookie，getCookie。
但是cookie也是不可以或缺的：cookie的作用是与服务器进行交互，作为HTTP规范的一部分而存在 ，而Web Storage仅仅是为了在本地“存储”数据而生
浏览器的支持除了IE７及以下不支持外，其他标准浏览器都完全支持(ie及FF需在web服务器里运行)，值得一提的是IE总是办好事，例如IE7、IE6中的userData其实就是javascript本地存储的解决方案。通过简单的代码封装可以统一到所有的浏览器都支持web storage。
localStorage和sessionStorage都具有相同的操作方法，例如setItem、getItem和removeItem等
### cookie 和session 的区别：
 1、cookie数据存放在客户的浏览器上，session数据放在服务器上。
 
 2、cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗
 
  考虑到安全应当使用session。
 
 3、session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能
 
  考虑到减轻服务器性能方面，应当使用COOKIE。
 
 4、单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。
 
 5、所以个人建议：
 
  将登陆信息等重要信息存放为SESSION
 
  其他信息如果需要保留，可以放在COOKIE中
## 二、js继承方式及其优缺点
### 原型链继承的缺点
一是字面量重写原型会中断关系，使用引用类型的原型，并且子类型还无法给超类型传递参数。
借用构造函数（类式继承）
借用构造函数虽然解决了刚才两种问题，但没有原型，则复用无从谈起。所以我们需要原型链+借用构造函数的模式，这种模式称为组合继承
### 组合式继承
组合式继承是比较常用的一种继承方法，其背后的思路是 使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承。这样，既通过在原型上定义方法实现了函数复用，又保证每个实例都有它自己的属性。
具体请看：JavaScript继承方式详解
## 三、谈谈浮动和清除浮动
浮动的框可以向左或向右移动，直到他的外边缘碰到包含框或另一个浮动框的边框为止。由于浮动框不在文档的普通流中，所以文档的普通流的块框表现得就像浮动框不存在一样。浮动的块框会漂浮在文档普通流的块框上。
浮动元素引起的问题：
（1）父元素的高度无法被撑开，影响与父元素同级的元素
 
（2）与浮动元素同级的非浮动元素（内联元素）会跟随其后
 
（3）若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构
解决方法：
使用CSS中的clear:both;属性来清除元素的浮动可解决2、3问题，对于问题1，添加如下样式，给父元素添加clearfix样式：
  .clearfix:after{content: ".";display: block;height: 0;clear: both;visibility: hidden;}
 
  .clearfix{display: inline-block;} /* for IE/Mac */
清除浮动的几种方法：
  1，额外标签法，<div style="clear:both;"></div>（缺点：不过这个办法会增加额外的标签使HTML结构看起来不够简洁。）
 
  2，使用after伪类
 
  #parent:after{
 
  content:".";
 
  height:0;
 
  visibility:hidden;
 
  display:block;
 
  clear:both;
 
  }
  3,浮动外部元素
 
  4,设置overflow为hidden或者auto
## 四、异步加载的方式有哪些？
   1. defer, 只支持IE，并行加载js文件，会按照页面上的script标签的顺序来执行。
   2. async:并行加载js文件，下载完成后立即执行，不会按照页面上的script标签的顺序执行。
   3. 创建script,插入到DOM中，加载完毕后callBack。
## 五、谈谈你对angular的理解
    angular多应用于数据交互比较多的模块，以及表单提交，他在数据的接受和数据的渲染方面特别的简单方便，同时在单一页面的跳转如tab切换等方面可以用他的路由，提高页面的性能和防止在页面较多时发生作用域的重叠和bug，最主要的是的一些指令可以帮我们完成很多的事情，也可以自定一些标签，和进行模块话的封装指令，AngularJS的directive，你输入特定数据，他就能输出相应UI视图。是一个比较完善的前端MVW框架，包含模板，数据双向绑定，路由，模块化，服务，依赖注入等所有功能，模板功能强大丰富，并且是声明式的，自带了丰富的 Angular 指令。
## 六、ES6的了解
新增模板字符串（为JavaScript提供了简单的字符串插值功能）、箭头函数（操作符左边为输入的参数，而右边则是进行的操作以及返回的值Inputs=>outputs。）、for-of（用来遍历数据—例如数组中的值。）arguments对象可被不定参数和默认参数完美代替。ES6将promise对象纳入规范，提供了原生的Promise对象。增加了let和const命令，用来声明变量。增加了块级作用域。let命令实际上就增加了块级作用域。ES6规定，var命令和function命令声明的全局变量，属于全局对象的属性；let命令、const命令、class命令声明的全局变量，不属于全局对象的属性。。还有就是引入module模块的概念 
## 七、用过哪些设计模式？
### 工厂模式：
主要好处就是可以消除对象间的耦合，通过使用工程方法而不是new关键字。将所有实例化的代码集中在一个位置防止代码重复。
 
  工厂模式解决了重复实例化的问题 ，但还有一个问题,那就是识别问题，因为根本无法 搞清楚他们到底是哪个对象的实例。
 
 
function createObject(name,age,profession){//集中实例化的函数var obj = new Object();
  obj.name = name;
  obj.age = age;
  obj.profession = profession;
  obj.move = function () {
  return this.name + ' at ' + this.age + ' engaged in ' + this.profession;
  };
  return obj;
}
var test1 = createObject('trigkit4',22,'programmer');//第一个实例var test2 = createObject('mike',25,'engineer');//第二个实例
 
### 构造函数模式
使用构造函数的方法 ，即解决了重复实例化的问题 ，又解决了对象识别的问题，该模式与工厂模式的不同之处在于：
1.构造函数方法没有显示的创建对象 (new Object());
 
2.直接将属性和方法赋值给 this 对象;
 
3.没有 renturn 语句。
## 八、说说你对闭包的理解
使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。在js中，函数即闭包，只有函数才会产生作用域的概念
闭包有三个特性：
1.函数嵌套函数
2.函数内部可以引用外部的参数和变量
3.参数和变量不会被垃圾回收机制回收
闭包通常用来创建内部变量，使得这些变量不能被外部随意修改，同时又可以通过指定的函数接口来操作。
## 九、DOM操作——怎样添加、移除、移动、复制、创建和查找节点。
1）创建新节点
  createDocumentFragment() //创建一个DOM片段
  createElement() //创建一个具体的元素
  createTextNode() //创建一个文本节点
2）添加、移除、替换、插入
  appendChild()
  removeChild()
  replaceChild()
  insertBefore() //并没有insertAfter()
3）查找
  getElementsByTagName() //通过标签名称
  getElementsByName() //通过元素的Name属性的值(IE容错能力较强，
  会得到一个数组，其中包括id等于name值的)
  getElementById() //通过元素Id，唯一性
## 十一、谈谈你对html5的理解
HTML5是对HTML标准的第五次修订。其主要目的就是将互联网语义化，以便更好的被人类和机器阅读，并同时提供更好的支持各种媒体的嵌入。HTML5的语法是向后兼容的。HTML5的设计目的是为了在移动设备上支持多媒体。新的语法特征被引进以支持这一点，如video、audio和canvas标记。HTML5还引进了新的功能，可以真正改变用户与文档的交互方式。HTML5手机应用的最大优势就是可以在网页上面直接调试和修改。原先应用的开发人员可能需要花费非常大的力气才能达到HTML5的效果，不断的重复编码、调试和运行，这是首先解决的一个问题。因此也有许多手机杂志客户端是基于HTML5标准，开发人员可以轻松调试修改。
## 十二、html5有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？
  HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
  拖拽释放(Drag and drop) API
  语义化更好的内容标签（header,nav,footer,aside,article,section）
  音频、视频API(audio,video)
  画布(Canvas) API
  地理(Geolocation) API
本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；
  sessionStorage 的数据在浏览器关闭后自动删除
  表单控件，calendar、date、time、email、url、search
  新的技术webworker, websocket, Geolocation
移除的元素
纯表现的元素：basefont，big，center，font, s，strike，tt，u；
对可用性产生负面影响的元素：frame，frameset，noframes；
支持HTML5新标签：
  IE8/IE7/IE6支持通过document.createElement方法产生的标签，
  可以利用这一特性让这些浏览器支持HTML5新标签，
  当然最好的方式是直接使用成熟的框架、使用最多的是html5shim框架
  <!--[if lt IE 9]>
  <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
  <![endif]-->
## 十三、如何实现浏览器内多个标签页之间的通信?
  调用localstorge、cookies等本地存储方式
## 十四、什么是 FOUC（无样式内容闪烁）？你如何来避免 FOUC？
  FOUC - Flash Of Unstyled Content 文档样式闪烁
  <style type="text/css" media="all">@import "../fouc.css";</style>
 
  而引用CSS文件的@import就是造成这个问题的罪魁祸首。IE会先加载整个HTML文档的DOM，然后再去导入外部的CSS文件，因此，在页面DOM加载完成到CSS导入完成中间会有一段时间页面上的内容是没有样式的，这段时间的长短跟网速，电脑速度都有关系。
 
  解决方法简单的出奇，只要在<head>之间加入一个<link>或者<script>元素就可以了。
## 十五、null和undefined的区别？
null是一个表示"无"的对象，转为数值时为0；undefined是一个表示"无"的原始值，转为数值时为NaN。
当声明的变量还未被初始化时，变量的默认值为undefined。
null用来表示尚未存在的对象，常用来表示函数企图返回一个不存在的对象。
undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是：
（1）变量被声明了，但没有赋值时，就等于undefined。
（2) 调用函数时，应该提供的参数没有提供，该参数等于undefined。
（3）对象没有赋值的属性，该属性的值为undefined。
（4）函数没有返回值时，默认返回undefined。
null表示"没有对象"，即该处不应该有值。典型用法是：
（1） 作为函数的参数，表示该函数的参数不是对象。
（2） 作为对象原型链的终点。
## 十六、new操作符具体干了什么呢?
  1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
  2、属性和方法被加入到 this 引用的对象中。
  3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。
var obj = {};
obj.__proto__ = Base.prototype;
Base.call(obj);
## 十七、哪些操作会造成内存泄漏？
内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。
垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。
setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
## 十八、异步加载和延迟加载
1.异步加载的方案： 动态插入script标签

2.通过ajax去获取js代码，然后通过eval执行
 
3.script标签上添加defer或者async属性
 
4.创建并插入iframe，让它异步执行js
 
5.延迟加载：有些 js 代码并不是页面初始化的时候就立刻需要的，而稍后的某些情况才需要的。
## 十九、ie各版本和chrome可以并行下载多少个资源
IE6 两个并发，iE7升级之后的6个并发，之后版本也是6个
Firefox，chrome也是6个
## 二十、Flash、Ajax各自的优缺点，在使用中如何取舍？
• Flash适合处理多媒体、矢量图形、访问机器；对CSS、处理文本上不足，不容易被搜索。
-Ajax对CSS、文本支持很好，支持搜索；多媒体、矢量图形、机器访问不足。
• 共同点：与服务器的无刷新传递消息、用户离线和在线状态、操作DOM
## 二十一、请解释一下 JavaScript 的同源策略。
概念:同源策略是客户端脚本（尤其是Javascript）的重要的安全度量标准。它最早出自Netscape Navigator2.0，其目的是防止某个文档或脚本从多个不同源装载。
这里的同源策略指的是：协议，域名，端口相同，同源策略是一种安全协议。
指一段脚本只能读取来自同一来源的窗口和文档的属性。
## 二十二、为什么要有同源限制？
我们举例说明：比如一个黑客程序，他利用Iframe把真正的银行登录页面嵌到他的页面上，当你使用真实的用户名，密码登录时，他的页面就可以通过Javascript读取到你的表单中input中的内容，这样用户名，密码就轻松到手了。
缺点：
现在网站的JS 都会进行压缩，一些文件用了严格模式，而另一些没有。这时这些本来是严格模式的文件，被 merge 后，这个串就到了文件的中间，不仅没有指示严格模式，反而在压缩后浪费了字节。
## 二十三、GET和POST的区别，何时使用POST？
  GET：一般用于信息获取，使用URL传递参数，对所发送信息的数量也有限制，一般在2000个字符
 
  POST：一般用于修改服务器上的资源，对所发送的信息没有限制。
 
 
  GET方式需要使用Request.QueryString来取得变量的值，而POST方式通过Request.Form来获取变量的值，
 
  也就是说Get是通过地址栏来传值，而Post是通过提交表单来传值。
 
 
 
然而，在以下情况中，请使用 POST 请求：
 
无法使用缓存文件（更新服务器上的文件或数据库）
 
向服务器发送大量数据（POST 没有数据量限制）
 
发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠
## 二十四、事件、IE与火狐的事件机制有什么区别？ 如何阻止冒泡？
 1. 我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。
 
 2. 事件处理机制：IE是事件冒泡、firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件。；
 
 3. `ev.stopPropagation()`;注意旧ie的方法 `ev.cancelBubble = true`;
## 二十五、ajax的缺点和在IE下的问题？
ajax的缺点
  1、ajax不支持浏览器back按钮。
 
  2、安全问题 AJAX暴露了与服务器交互的细节。
 
  3、对搜索引擎的支持比较弱。
 
  4、破坏了程序的异常机制。
 
  5、不容易调试。
### IE缓存问题
在IE浏览器下，如果请求的方法是GET，并且请求的URL不变，那么这个请求的结果就会被缓存。解决这个问题的办法可以通过实时改变请求的URL，只要URL改变，就不会被缓存，可以通过在URL末尾添加上随机的时间戳参数('t'= + new Date().getTime())
或者：
open('GET','demo.php?rand=+Math.random()',true);//
Ajax请求的页面历史记录状态问题
可以通过锚点来记录状态，location.hash。让浏览器记录Ajax请求时页面状态的变化。
还可以通过HTML5的history.pushState，来实现浏览器地址栏的无刷新改变
 HTTP状态码
  100 Continue 继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息
 
  200 OK 正常返回信息
 
  201 Created 请求成功并且服务器创建了新的资源
 
  202 Accepted 服务器已接受请求，但尚未处理
 
  301 Moved Permanently 请求的网页已永久移动到新位置。
 
  302 Found 临时性重定向。
 
  303 See Other 临时性重定向，且总是使用 GET 请求新的 URI。
 
  304 Not Modified 自从上次请求后，请求的网页未修改过。
 
  400 Bad Request 服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发起请求。
 
  401 Unauthorized 请求未授权。
 
  403 Forbidden 禁止访问。
 
  404 Not Found 找不到如何与 URI 相匹配的资源。
 
  500 Internal Server Error 最常见的服务器端错误。
 
  503 Service Unavailable 服务器端暂时无法处理请求（可能是过载或维护）。
 实现一个函数clone，可以对JavaScript中的5种主要的数据类型（包括Number、String、Object、Array、Boolean）进行值复制
  Object.prototype.clone = function(){
 
  var o = this.constructor === Array ? [] : {};
 
  for(var e in this){
 
  o[e] = typeof this[e] === "object" ? this[e].clone() : this[e];
 
  }
说说你对AMD和Commonjs的理解
CommonJS是服务器端模块的规范，Node.js采用了这个规范。CommonJS规范加载模块是同步的，也就是说，只有加载完成，才能执行后面的操作。AMD规范则是非同步加载模块，允许指定回调函数。
AMD推荐的风格通过返回一个对象做为模块对象，CommonJS的风格通过对module.exports或exports的属性赋值来达到暴露模块对象的目的。
 
  return o;
  }
document.write()的用法
document.write()方法可以用在两个方面：页面载入过程中用实时脚本创建页面内容，以及用延时脚本创建本窗口或新窗口的内容。
document.write只能重绘整个页面。innerHTML可以重绘页面的一部分
说说严格模式的限制
严格模式主要有以下限制：
变量必须声明后再使用
 
函数的参数不能有同名属性，否则报错
 
不能使用with语句
 
不能对只读属性赋值，否则报错
 
不能使用前缀0表示八进制数，否则报错
 
不能删除不可删除的属性，否则报错
 
不能删除变量delete prop，会报错，只能删除属性delete global[prop]
 
eval不会在它的外层作用域引入变量
 
eval和arguments不能被重新赋值
 
arguments不会自动反映函数参数的变化
 
不能使用arguments.callee
 
不能使用arguments.caller
 
禁止this指向全局对象
 
不能使用fn.caller和fn.arguments获取函数调用的堆栈
 
增加了保留字（比如protected、static和interface）
设立"严格模式"的目的，主要有以下几个：
消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;
消除代码运行的一些不安全之处，保证代码运行的安全；
提高编译器效率，增加运行速度；
为未来新版本的Javascript做好铺垫。
注：经过测试IE6,7,8,9均不支持严格模式。
说说mongoDB和MySQL的区别
MySQL是传统的关系型数据库，MongoDB则是非关系型数据库
mongodb以BSON结构（二进制）进行存储，对海量数据存储有着很明显的优势。
对比传统关系型数据库,NoSQL有着非常显著的性能和扩展性优势，与关系型数据库相比，MongoDB的优点有： ①弱一致性（最终一致），更能保证用户的访问速度： ②文档结构的存储方式，能够更便捷的获取数据。
讲讲304缓存的原理
服务器首先产生ETag，服务器可在稍后使用它来判断页面是否已经被修改。本质上，客户端通过将该记号传回服务器要求服务器验证其（客户端）缓存。
 
304是HTTP状态码，服务器用来标识这个文件没修改，不返回内容，浏览器在接收到个状态码后，会使用浏览器已缓存的文件
 
客户端请求一个页面（A）。 服务器返回页面A，并在给A加上一个ETag。 客户端展现该页面，并将页面连同ETag一起缓存。 客户再次请求页面A，并将上次请求时服务器返回的ETag一起传递给服务器。 服务器检查该ETag，并判断出该页面自上次客户端请求之后还未被修改，直接返回响应304（未修改——Not Modified）和一个空的响应体。
 
什么样的前端代码是好的
高复用低耦合，这样文件小，好维护，而且好扩展。
当你把地址发送给后台之后，发生了哪些过程？
1.浏览器根据请求的url叫个DNS域名解析，找到真实的ip，向服务器发起请求
2服务器交给后台处理后返回数据，浏览器接收数据
3，浏览器对解析到的数据进行解析，建立相应的数据结构dom
4载入解析到的资源渲染页面，完成
什么是跨域？跨域有哪几种方法？
1.利用有scr属性的标签进行跨域，如script,iframe,img等，
2.利用<script>标签没有跨域限制的“漏洞”（历史遗迹啊）来达到与第三方通讯的目的。
原理：json是Jewavascript中的对象，而跨域访问中有图片、css、javascript脚本文件等是不受限制的，因此你可以在页面渲染时动态在<script>标签设置src路径，而这个路径返回回来的就是json对象。
如何解决跨域问题
### JSONP：
原理是：动态插入script标签，通过script标签引入一个js文件，这个js文件载入成功后会执行我们在url参数中指定的函数，并且会把我们需要的json数据作为参数传入。
由于同源策略的限制，XmlHttpRequest只允许请求当前源（域名、协议、端口）的资源，为了实现跨域请求，可以通过script标签实现跨域请求，然后在服务端输出JSON数据并执行回调函数，从而解决了跨域的数据请求。
优点是兼容性好，简单易用，支持浏览器与服务器双向通信。缺点是只支持GET请求。
JSONP：json+padding（内填充），顾名思义，就是把JSON填充到一个盒子里
<script>
  function createJs(sUrl){
 
  var oScript = document.createElement('script');
  oScript.type = 'text/javascript';
  oScript.src = sUrl;
  document.getElementsByTagName('head')[0].appendChild(oScript);
  }
 
  createJs('jsonp.js');
 
  box({
  'name': 'test'
  });
 
  function box(json){
  alert(json.name);
  }</script>
CORS
服务器端对于CORS的支持，主要就是通过设置Access-Control-Allow-Origin来进行的。如果浏览器检测到相应的设置，就可以允许Ajax进行跨域的访问。
通过修改document.domain来跨子域
将子域和主域的document.domain设为同一个主域.前提条件：这两个域名必须属于同一个基础域名!而且所用的协议，端口都要一致，否则无法利用document.domain进行跨域
主域相同的使用document.domain
使用window.name来进行跨域
window对象有个name属性，该属性有个特征：即在一个窗口(window)的生命周期内,窗口载入的所有的页面都是共享一个window.name的，每个页面对window.name都有读写的权限，window.name是持久存在一个窗口载入过的所有页面中的
使用HTML5中新引进的window.postMessage方法来跨域传送数据
还有flash、在服务器上设置代理页面等跨域方式。个人认为window.name的方法既不复杂，也能兼容到几乎所有浏览器，这真是极好的一种跨域方法。

### XML和JSON的区别？
(1).数据体积方面。
 
JSON相对于XML来讲，数据的体积小，传递的速度更快些。
 
(2).数据交互方面。
 
JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互。
 
(3).数据描述方面。
 
JSON对数据的描述性比XML较差。
 
(4).传输速度方面。
 
JSON的速度要远远快于XML。
### 谈谈你对webpack的看法
WebPack 是一个模块打包工具，你可以使用WebPack管理你的模块依赖，并编绎输出模块们所需的静态文件。它能够很好地管理、打包Web开发中所用到的HTML、Javascript、CSS以及各种静态文件（图片、字体等），让开发过程更加高效。对于不同类型的资源，webpack有对应的模块加载器。webpack模块打包器会分析模块间的依赖关系，最后 生成了优化且合并后的静态资源。
webpack的两大特色：
1.code splitting（可以自动完成）
 
2.loader 可以处理各种类型的静态文件，并且支持串联操作
webpack 是以commonJS的形式来书写脚本滴，但对 AMD/CMD 的支持也很全面，方便旧项目进行代码迁移。
webpack具有requireJs和browserify的功能，但仍有很多自己的新特性：
1. 对 CommonJS 、 AMD 、ES6的语法做了兼容
 
2. 对js、css、图片等资源文件都支持打包
 
3. 串联式模块加载器以及插件机制，让其具有更好的灵活性和扩展性，例如提供对CoffeeScript、ES6的支持
 
4. 有独立的配置文件webpack.config.js
 
5. 可以将代码切割成不同的chunk，实现按需加载，降低了初始化时间
 
6. 支持 SourceUrls 和 SourceMaps，易于调试
 
7. 具有强大的Plugin接口，大多是内部插件，使用起来比较灵活
 
8.webpack 使用异步 IO 并具有多级缓存。这使得 webpack 很快且在增量编译上更加快
position的值， relative和absolute分别是相对于谁进行定位的？
absolute :生成绝对定位的元素， 相对于最近一级的 定位不是 static 的父元素来进行定位。

fixed （老IE不支持）生成绝对定位的元素，通常相对于浏览器窗口或 frame 进行定位。

relative 生成相对定位的元素，相对于其在普通流中的位置进行定位。

static 默认值。没有定位，元素出现在正常的流中

sticky 生成粘性定位的元素，容器的位置根据正常文档流计算得出
 
