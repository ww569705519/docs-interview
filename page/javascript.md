## JavaScript


### 介绍js的基本数据类型。

Undefined、Null、Boolean、Number、String

!> ECMAScript 2015 新增:Symbol(创建后独一无二且不可变的数据类型 )

### 介绍js有哪些内置对象？

Object 是 JavaScript 中所有对象的父对象

数据封装类对象：Object、Array、Boolean、Number 和 String
其他对象：Function、Arguments、Math、Date、RegExp、Error

参考：http://www.ibm.com/developerworks/cn/web/wa-objectsinjs-v1b/index.html

### 说几条写JavaScript的基本规范？

1. 不要在同一行声明多个变量。
2. 请使用 ===/!==来比较true/false或者数值
3. 使用对象字面量替代new Array这种形式
4. 不要使用全局函数。
5. Switch语句必须带有default分支
6. 函数不应该有时候有返回值，有时候没有返回值。
7. For循环必须使用大括号
8. If语句必须使用大括号
9. for-in循环中的变量 应该使用var关键字明确限定作用域，从而避免作用域污染。

### JavaScript原型，原型链 ? 有什么特点？

每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，
如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，
于是就这样一直找下去，也就是我们平时所说的原型链的概念。

**特点：**

JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。


当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的话，
就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象。
```js
function Func(){}
Func.prototype.name = "Sean";
Func.prototype.getInfo = function() {
  return this.name;
}
var person = new Func();//现在可以参考var person = Object.create(oldObject);
console.log(person.getInfo());//它拥有了Func的属性和方法
//"Sean"
console.log(Func.prototype);
// Func { name="Sean", getInfo=function()}
```



### JavaScript有几种类型的值？

javascript有两种类型的值，分别是数据类型和引用类型。

原始数据类型（Undefined，Null，Boolean，Number、String）

引用数据类型（对象、数组和函数）

### 如何将字符串转化为数字，例如'12.3b'?

* parseFloat('12.3b');
* 正则表达式，'12.3b'.match(/(\d)+(\.)?(\d)+/g)[0] * 1, 但是这个不太靠谱，提供一种思路而已。

### 如何将浮点数点左边的数每三位添加一个逗号，如12000000.11转化为『12,000,000.11』?
```js
function commafy(num){
	return num && num
		.toString()
		.replace(/(\d)(?=(\d{3})+\.)/g, function($1, $2){
			return $2 + ',';
		});
}
```

### Javascript如何实现继承？

1. 构造继承
2. 原型继承
3. 实例继承
4. 拷贝继承

原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式。
```js
function Parent(){
	this.name = 'wang';
}

function Child(){
	this.age = 28;
}
Child.prototype = new Parent();//继承了Parent，通过原型

var demo = new Child();
alert(demo.age);
alert(demo.name);//得到被继承的属性
```

### JavaScript继承的几种实现方式？
  - 参考：[构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)，[非构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)；


### javascript创建对象的几种方式？

javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用。


1. 对象字面量的方式
```js
	person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};
```

2. 用function来模拟无参的构造函数
```js
	function Person(){}
	var person=new Person();//定义一个function，如果使用new"实例化",该function可以看作是一个Class
	person.name="Mark";
	person.age="25";
	person.work=function(){
	alert(person.name+" hello...");
	}
	person.work();
```

3. 用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）
```js
	function Pet(name,age,hobby){
	   this.name=name;//this作用域：当前对象
	   this.age=age;
	   this.hobby=hobby;
	   this.eat=function(){
	      alert("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");
	   }
	}
	var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象
	maidou.eat();//调用eat方法
```

4. 用工厂方式来创建（内置对象）

	 var wcDog =new Object();
	 wcDog.name="旺财";
	 wcDog.age=3;
	 wcDog.work=function(){
	   alert("我是"+wcDog.name+",汪汪汪......");
	 }
	 wcDog.work();


5. 用原型方式来创建
```js
	function Dog(){

	 }
	 Dog.prototype.name="旺财";
	 Dog.prototype.eat=function(){
	 alert(this.name+"是个吃货");
	 }
	 var wangcai =new Dog();
	 wangcai.eat();
```

5. 用混合方式来创建
```js
	function Car(name,price){
	  this.name=name;
	  this.price=price;
	}
	 Car.prototype.sell=function(){
	   alert("我是"+this.name+"，我现在卖"+this.price+"万元");
	  }
	var camry =new Car("凯美瑞",27);
	camry.sell();
```

### Javascript作用链域?

全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。

当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，
直至全局函数，这种组织形式就是作用域链。

### 谈谈This对象的理解。

* this总是指向函数的直接调用者（而非间接调用者）；
* 如果有new关键字，this指向new出来的那个对象；
* 在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent中的this总是指向全局对象Window；


### eval是做什么的？

它的功能是把对应的字符串解析成JS代码并运行；

!> 应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。
由JSON字符串转换为JSON对象的时候可以用eval，var obj =eval('('+ str +')');

### 什么是window对象? 什么是document对象?

window对象是指浏览器打开的窗口。

document对象是Documentd对象（HTML 文档对象）的一个只读引用，window对象的一个属性。

### null，undefined 的区别？

null 		表示一个对象是“没有值”的值，也就是值为“空”；

undefined 	表示一个变量声明了没有初始化(赋值)；

* undefined不是一个有效的JSON，而null是；
* undefined的类型(typeof)是undefined；
* null的类型(typeof)是object；


* Javascript将未赋值的变量默认值设为undefined；
* Javascript从来不会将变量设为null。它是用来让程序员表明某个用var声明的变量时没有值的。

```js
typeof undefined
	//"undefined"
	undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined；
	例如变量被声明了，但没有赋值时，就等于undefined

typeof null
	//"object"
	null : 是一个对象(空对象, 没有任何属性和方法)；
	例如作为函数的参数，表示该函数的参数不是对象；
```

!> 注意：在验证null时，一定要使用　=== ，因为 == 无法分别 null 和　undefined


```js		
	null == undefined // true
	null === undefined // false
```

### 事件是？IE与火狐的事件机制有什么区别？ 如何阻止冒泡？

 1. 我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。
 2. 事件处理机制：IE是事件冒泡、Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件；
 3. ev.stopPropagation();（旧ie的方法 ev.cancelBubble = true;）


### 什么是闭包（closure），为什么要用它？

**闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量,利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。**

闭包的特性：

1. 函数内再嵌套函数
2. 内部函数可以引用外层的参数和变量
3. 参数和变量不会被垃圾回收机制回收

```html
<!-- li节点的onclick事件都能正确的弹出当前被点击的li索引 -->

 <ul id="testUL">
    <li> index = 0</li>
    <li> index = 1</li>
    <li> index = 2</li>
    <li> index = 3</li>
</ul>
<script type="text/javascript">
  	var nodes = document.getElementsByTagName("li");
	for(i = 0;i<nodes.length;i+= 1){
	    nodes[i].onclick = (function(i){
	              return function() {
	                 console.log(i);
	              } //不用闭包的话，值每次都是4
	            })(i);
	}
</script>
```

执行`say667()`后,`say667()`闭包内部变量会存在,而闭包内部函数的内部变量不会存在
使得`Javascript`的垃圾回收机制GC不会收回`say667()`所占用的资源
因为`say667()`的内部函数的执行需要依赖`say667()`中的变量
这是对闭包作用的非常直白的描述
```js
  function say667() {
	// Local variable that ends up within closure
	var num = 666;
	var sayAlert = function() {
		alert(num);
	}
	num++;
	return sayAlert;
}

 var sayAlert = say667();
 sayAlert()//执行结果应该弹出的667
```

### javascript 代码中的"use strict";是什么意思 ? 使用它区别是什么？

use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行,

* 使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为。
* 默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值;
* 全局变量的显示声明,函数必须声明在顶层，不允许在非函数代码块内声明函数,arguments.callee也不允许使用；
* 消除代码运行的一些不安全之处，保证代码运行的安全,限制函数中的arguments修改，严格模式下的eval函数的行为和非严格模式的也不相同;
* 提高编译器效率，增加运行速度；
* 为未来新版本的Javascript标准化做铺垫。


### 如何判断一个对象是否属于某个类？

使用`instanceof`
```js
if(a instanceof Person){
	alert('yes');
}
```

### new操作符具体干了什么呢?

1. 创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。
2. 属性和方法被加入到 this 引用的对象中。
3. 新创建的对象由 this 所引用，并且最后隐式的返回 this 。
```js
	var obj  = {};
	obj.__proto__ = Base.prototype;
	Base.call(obj);
```


### Javascript中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？

**hasOwnProperty**

javaScript中hasOwnProperty函数方法是返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性；该属性必须是对象本身的一个成员。

**使用方法：**`object.hasOwnProperty(proName)`


其中参数object是必选项。一个对象的实例。

proName是必选项。一个属性名称的字符串值。

如果 object 具有指定名称的属性，那么JavaScript中hasOwnProperty函数方法返回 true，反之则返回 false。

### JSON 的了解？

**JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。**

它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小
如：{"age":"12", "name":"back"}

JSON字符串转换为JSON对象:
```js
var obj =eval('('+ str +')');
var obj = str.parseJSON();
var obj = JSON.parse(str);
```

JSON对象转换为JSON字符串：
```js
var last=obj.toJSONString();
var last=JSON.stringify(obj);
```

### js延迟加载的方式有哪些？

* `defer`和`async` 
* 动态创建DOM方式（用得最多）
* 按需异步载入js


### Ajax 是什么? 如何创建一个Ajax？

ajax的全称：`Asynchronous Javascript And XML。`

**所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。**

1. 创建XMLHttpRequest对象,也就是创建一个异步调用对象
2. 创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息
3. 设置响应HTTP请求状态变化的函数
4. 发送HTTP请求
5. 获取异步调用返回的数据
6. 使用JavaScript和DOM实现局部刷新

### 同步和异步的区别?

同步：浏览器访问服务器请求，用户看得到页面刷新，重新发请求,等请求完，页面刷新，新内容出现，用户看到新内容,进行下一步操作。

异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求。等请求完，页面不刷新，新内容也会出现，用户看到新内容。

### 如何解决跨域问题?

**jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面**

### AMD（Modules/Asynchronous-Definition）、CMD（Common Module Definition）规范区别？

> AMD 规范在这里：https://github.com/amdjs/amdjs-api/wiki/AMD

> CMD 规范在这里：https://github.com/seajs/seajs/issues/242

Asynchronous Module Definition，异步模块定义，所有的模块将被异步加载，模块加载不影响后面语句运行。所有依赖某些模块的语句均放置在回调函数中。

区别：

1. 对于依赖的模块，AMD 是提前执行，CMD 是延迟执行。不过 RequireJS 从 2.0 开始，也改成可以延迟执行（根据写法不同，处理方式不同）。CMD 推崇 as lazy as possible.
2. CMD 推崇依赖就近，AMD 推崇依赖前置。看代码：

```js
// CMD
define(function(require, exports, module) {
    var a = require('./a')
    a.doSomething()
    // 此处略去 100 行
    var b = require('./b') // 依赖可以就近书写
    b.doSomething()
    // ...
})

// AMD 默认推荐
define(['./a', './b'], function(a, b) { // 依赖必须一开始就写好
    a.doSomething()
    // 此处略去 100 行
    b.doSomething()
    // ...
})
```

### 异步加载JS的方式有哪些？

1. defer，只支持IE

2. async：

3. 创建script，插入到DOM中，加载完毕后callBack

### documen.write和 innerHTML的区别

document.write只能重绘整个页面

innerHTML可以重绘页面的一部分

### DOM操作——怎样添加、移除、移动、复制、创建和查找节点?

1. 创建新节点
	createDocumentFragment()    //创建一个DOM片段
	createElement()   //创建一个具体的元素
	createTextNode()   //创建一个文本节点
2. 添加、移除、替换、插入
	appendChild()
	removeChild()
	replaceChild()
	insertBefore() //在已有的子节点前插入一个新的子节点
3. 查找
	getElementsByTagName()    //通过标签名称
	getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
	getElementById()    //通过元素Id，唯一性

### .call() 和 .apply() 的区别？


例子中用 add 来替换 sub，add.call(sub,3,1) == add(3,1) ，所以运行结果为：alert(4);

注意：js 中的函数其实是对象，函数名是对 Function 对象的引用。

```js
	function add(a,b)
	{
	    alert(a+b);
	}

	function sub(a,b)
	{
	    alert(a-b);
	}

	add.call(sub,3,1);
```


### 那些操作会造成内存泄漏？

内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。
垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。

setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

### Object.is() 与原来的比较操作符“ ===”、“ ==”的区别？

两等号判等，会在比较时进行类型转换；
三等号判等(判断严格)，比较时不进行隐式类型转换,（类型不同则会返回false）；

Object.is 在三等号判等的基础上特别处理了 NaN 、-0 和 +0 ，保证 -0 和 +0 不再相同，
但 Object.is(NaN, NaN) 会返回 true.

Object.is 应被认为有其特殊的用途，而不能用它认为它比其它的相等对比更宽松或严格。

### 什么叫优雅降级和渐进增强？

优雅降级：Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会针对旧版本的IE进行降级处理了,使之在旧式浏览器上以某种形式降级体验却不至于完全不能用。
如：border-shadow

渐进增强：从被所有浏览器支持的基本功能开始，逐步地添加那些只有新版本浏览器才支持的功能,向页面增加不影响基础浏览器的额外样式和功能的。当浏览器支持时，它们会自动地呈现出来并发挥作用。
如：默认使用flash上传，但如果浏览器支持 HTML5 的文件上传功能，则使用HTML5实现更好的体验；


### 对Node的优点和缺点提出了自己的看法？


*（优点）因为Node是基于事件驱动和无阻塞的，所以非常适合处理并发请求，
  因此构建在Node上的代理服务器相比其他技术实现（如Ruby）的服务器表现要好得多。
  此外，与Node代理服务器交互的客户端代码是由javascript语言编写的，
  因此客户端和服务器端都用同一种语言编写，这是非常美妙的事情。

*（缺点）Node是一个相对新的开源项目，所以不太稳定，它总是一直在变，
  而且缺少足够多的第三方库支持。看起来，就像是Ruby/Rails当年的样子。






- 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？（流程说的越详细越好）

		  注：这题胜在区分度高，知识点覆盖广，再不懂的人，也能答出几句，
		  而高手可以根据自己擅长的领域自由发挥，从URL规范、HTTP协议、DNS、CDN、数据库查询、
		  到浏览器流式解析、CSS规则构建、layout、paint、onload/domready、JS执行、JS API绑定等等；

		  详细版：
			1、浏览器会开启一个线程来处理这个请求，对 URL 分析判断如果是 http 协议就按照 Web 方式来处理;
			2、调用浏览器内核中的对应方法，比如 WebView 中的 loadUrl 方法;
		    3、通过DNS解析获取网址的IP地址，设置 UA 等信息发出第二个GET请求;
			4、进行HTTP协议会话，客户端发送报头(请求报头);
		    5、进入到web服务器上的 Web Server，如 Apache、Tomcat、Node.JS 等服务器;
		    6、进入部署好的后端应用，如 PHP、Java、JavaScript、Python 等，找到对应的请求处理;
			7、处理结束回馈报头，此处如果浏览器访问过，缓存上有对应资源，会与服务器最后修改时间对比，一致则返回304;
		    8、浏览器开始下载html文档(响应报头，状态码200)，同时使用缓存;
		    9、文档树建立，根据标记请求所需指定MIME类型的文件（比如css、js）,同时设置了cookie;
		    10、页面开始渲染DOM，JS根据DOM API操作DOM,执行事件绑定等，页面显示完成。

		  简洁版：
			浏览器根据请求的URL交给DNS域名解析，找到真实IP，向服务器发起请求；
			服务器交给后台处理完成后返回数据，浏览器接收文件（HTML、JS、CSS、图象等）；
			浏览器对加载到的资源（HTML、JS、CSS等）进行语法解析，建立相应的内部数据结构（如HTML的DOM）；
			载入解析到的资源文件，渲染页面，完成。
