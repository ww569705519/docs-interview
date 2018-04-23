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

**原型**

每个对象都会在其内部初始化一个属性，就是prototype(原型)。

**原型链**

当我们访问一个对象的属性时，
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


### javascript创建对象的几种方式？

#### 工厂模式

工厂模式是软件工程领域一种广为人知的设计模式



```js
function createPerson(name, age, job){
	var o = new Object();
	o.name = name;
	o.age = age;
	o.job = job;
	o.sayName = function(){
	alert(this.name);
	};
	return o;
}
var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor"); 

```
优点

**这种模式抽象了创建具体对象的过程**

弊端

**没有解决对象识别的问题（即怎样知道一个对象的类型）**

#### 构造函数模式

```js
function Person(name, age, job){
 this.name = name;
 this.age = age;
 this.job = job;
 this.sayName = function(){
 alert(this.name);
 };
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor"); 
```

与工厂模式相比

* 没有显式地创建对象
* 直接将属性和方法赋给了 `this` 对象
* 没有 return 语句

要创建 Person 的新实例，必须使用 new 操作符。以这种方式调用构造函数实际上会经历以下 4 个步骤：

1. 创建一个新对象
2. 将构造函数的作用域赋给新对象(因此 `this` 就指向了这个新对象)
3. 执行构造函数中的代码(为这个新对象添加属性)
4. 返回新对象

缺点

**每个方法都有在每个实例上重新创建一遍。person1和person2都有一个sayName()的方法，但两个方法不是同一个Function实例。不同实例上的同名函数是不相等的。**

**创建两个完成同样任务的Function实例没有必要，而且还有this对象在，不需要在执行代码前就把函数绑定在特定对象上，可以像下面这样。**


```js
function Person(name, age, job){
	this.name = name;
	this.age = age;
	this.job = job;
	this.sayName = sayName;
}
function sayName(){
	alert(this.name);
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor"); 
```

*把sayName属性设置成全局的sayName函数，这样，由于sayName包含的是一个指向函数的指针，因此person1和person2对象就共享了同一个函数。*

#### 原型模式

理解原型对象 

**我们创建的每个函数都有一个prototype属性，这个属性是一个指针，指向一个对象，而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。prototype是通过调用构造函数而创建的那个对象实例的对象原型，使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法。**

```js
function Person(){
}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function(){
	alert(this.name);
};
var person1 = new Person(); 
```

原型对象的问题 

**原型模式最大问题是由其共享的本性所导致的。**

**对于包含引用类型值的属性来说，问题较为突出**


#### 组合使用构造模式和原型模式

创建自定义类型的最常见方式，就是组合使用构造函数模式与原型模式。构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。

```js
function Person(name, age, job){
	this.name = name;
	this.age = age;
	this.job = job;
	this.friends = ["Shelby", "Court"];
}
Person.prototype = {
	constructor : Person,
	sayName : function(){
	alert(this.name);
 }
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
person1.friends.push("Van");
alert(person1.friends); //"Shelby,Count,Van"
alert(person2.friends); //"Shelby,Count"
alert(person1.friends === person2.friends); //false
alert(person1.sayName === person2.sayName); //true 
```

#### 动态原型模式
#### 寄生构造模式
#### 稳妥构造模式

*由于以上模式使用频率过低，故不多做撰述*

### Javascript如何实现继承？

#### 原型链

**基本思想：利用原型让一个引用类型继承另外一个引用类型的属性和方法。**

**构造函数，原型，实例之间的关系：每个构造函数都有一个原型对象，原型对象包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。**

原型链实现继承例子：
```js
function SuperType() {
	this.property = true;
}
SuperType.prototype.getSuperValue = function() {
	return this.property;
}
function subType() {
	this.property = false;
}
//继承了SuperType
SubType.prototype = new SuperType();
SubType.prototype.getSubValue = function (){
	return this.property;
}
var instance = new SubType();
console.log(instance.getSuperValue());//true
```

#### 借用构造函数

**基本思想：在子类型构造函数的内部调用超类构造函数，通过使用call()和apply()方法可以在新创建的对象上执行构造函数。**

```js
function SuperType() {
	this.colors = ["red","blue","green"];
}
function SubType() {
	SuperType.call(this);//继承了SuperType
}
var instance1 = new SubType();
instance1.colors.push("black");
console.log(instance1.colors);//"red","blue","green","black"
var instance2 = new SubType();
console.log(instance2.colors);//"red","blue","green"
```

#### 组合继承

**基本思想：将原型链和借用构造函数的技术组合在一块，从而发挥两者之长的一种继承模式。**

```js
function SuperType(name) {
	this.name = name;
	this.colors = ["red","blue","green"];
}
SuperType.prototype.sayName = function() {
	console.log(this.name);
}
function SubType(name, age) {
	SuperType.call(this,name);//继承属性
	this.age = age;
}
//继承方法
SubType.prototype = new SuperType();
Subtype.prototype.constructor = Subtype;
Subtype.prototype.sayAge = function() {
	console.log(this.age);
}
var instance1 = new SubType("EvanChen",18);
instance1.colors.push("black");
consol.log(instance1.colors);//"red","blue","green","black"
instance1.sayName();//"EvanChen"
instance1.sayAge();//18
var instance2 = new SubType("EvanChen666",20);
console.log(instance2.colors);//"red","blue","green"
instance2.sayName();//"EvanChen666"
instance2.sayAge();//20
```

#### 原型式继承

**基本想法：借助原型可以基于已有的对象创建新对象，同时还不必须因此创建自定义的类型。**

原型式继承的思想可用以下函数来说明：
```js
function object(o) {
function F(){}
F.prototype = o;
return new F();
}
```

```js
var person = {
name:"EvanChen",
friends:["Shelby","Court","Van"];
};
var anotherPerson = object(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");
var yetAnotherPerson = object(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");
console.log(person.friends);//"Shelby","Court","Van","Rob","Barbie"
```

ECMAScript5通过新增Object.create()方法规范化了原型式继承，这个方法接收两个参数：一个用作新对象原型的对象和一个作为新对象定义额外属性的对象。

```js
var person = {
name:"EvanChen",
friends:["Shelby","Court","Van"];
};
var anotherPerson = Object.create(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");
var yetAnotherPerson = Object.create(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");
console.log(person.friends);//"Shelby","Court","Van","Rob","Barbie"
```

#### 寄生式继承

**基本思想：创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真正是它做了所有工作一样返回对象。**

```js
function createAnother(original) {
var clone = object(original);
clone.sayHi = function () {
alert("hi");
};
return clone;
}
var person = {
name:"EvanChen",
friends:["Shelby","Court","Van"];
};
var anotherPerson = createAnother(person);
anotherPerson.sayHi();///"hi"
```

#### 寄生组合式继承

**基本思想：通过借用函数来继承属性，通过原型链的混成形式来继承方法**

```js
function inheritProperty(subType, superType) {
var prototype = object(superType.prototype);//创建对象
prototype.constructor = subType;//增强对象
subType.prototype = prototype;//指定对象
}
```

例子

```js
function SuperType(name){
	this.name = name;
	this.colors = ["red","blue","green"];
}
SuperType.prototype.sayName = function (){
	alert(this.name);
};
function SubType(name,age){
	SuperType.call(this,name);
	this.age = age;
}
inheritProperty(SubType,SuperType);
SubType.prototype.sayAge = function() {
	alert(this.age);
}
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
	* createDocumentFragment()    //创建一个DOM片段
	* createElement()   //创建一个具体的元素
	* createTextNode()   //创建一个文本节点
2. 添加、移除、替换、插入
	* appendChild()
	* removeChild()
	* replaceChild()
	* insertBefore() //在已有的子节点前插入一个新的子节点
3. 查找
	* getElementsByTagName()    //通过标签名称
	* getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
	* getElementById()    //通过元素Id，唯一性

### .call() 和 .apply() 的区别？

**call 和 apply 都是为了改变某个函数运行时的 `context` 即上下文而存在的，换句话说，就是为了改变函数体内部 this 的指向**

`apply`：调用一个对象的一个方法，用另一个对象替换当前对象。例如：`B.apply(A, arguments);`即A对象应用B对象的方法。

`call`：调用一个对象的一个方法，用另一个对象替换当前对象。例如：`B.call(A, args1,args2);`即A对象调用B对象的方法。

**共同处**

都“可以用来代替另一个对象调用一个方法，将一个函数的对象上下文从初始的上下文改变为由thisObj指定的新对象”。

**不同之处**

apply：最多只能有两个参数——新this对象和一个数组argArray。如果给该方法传递多个参数，则把参数都写进这个数组里面，当然，即使只有一个参数，也要写进数组里。如果argArray不是一个有效的数组或arguments对象，那么将导致一个TypeError。如果没有提供argArray和thisObj任何一个参数，那么Global对象将被用作thisObj，并且无法被传递任何参数。

call：它可以接受多个参数，第一个参数与apply一样，后面则是一串参数列表。这个方法主要用在js对象各方法相互调用的时候，使当前this实例指针保持一致，或者在特殊情况下需要改变this指针。如果没有提供thisObj参数，那么 Global 对象被用作thisObj。 

**实际上，apply和call的功能是一样的，只是传入的参数列表形式不同。**


### 那些操作会造成内存泄漏？

内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。
垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。

**setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。
闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）**

### Object.is() 与原来的比较操作符“ ===”、“ ==”的区别？

两等号判等，会在比较时进行类型转换；
三等号判等(判断严格)，比较时不进行隐式类型转换,（类型不同则会返回false）；

Object.is 在三等号判等的基础上特别处理了 NaN 、-0 和 +0 ，保证 -0 和 +0 不再相同，
但 Object.is(NaN, NaN) 会返回 true.

Object.is 应被认为有其特殊的用途，而不能用它认为它比其它的相等对比更宽松或严格。

### 什么叫优雅降级和渐进增强？

**渐进增强**

针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。

**优雅降级**

一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。


### 对Node的优点和缺点提出了自己的看法？


*（优点）因为Node是基于事件驱动和无阻塞的，所以非常适合处理并发请求，
  因此构建在Node上的代理服务器相比其他技术实现（如Ruby）的服务器表现要好得多。
  此外，与Node代理服务器交互的客户端代码是由javascript语言编写的，
  因此客户端和服务器端都用同一种语言编写，这是非常美妙的事情。

*（缺点）Node是一个相对新的开源项目，所以不太稳定，它总是一直在变，
  而且缺少足够多的第三方库支持。看起来，就像是Ruby/Rails当年的样子。






## 一个页面从输入 URL 到页面加载显示完成，这个过程中都发生了什么？（流程说的越详细越好）

注：这题胜在区分度高，知识点覆盖广，再不懂的人，也能答出几句，
而高手可以根据自己擅长的领域自由发挥，从URL规范、HTTP协议、DNS、CDN、数据库查询、
到浏览器流式解析、CSS规则构建、layout、paint、onload/domready、JS执行、JS API绑定等等；

**详细版**
1. 浏览器会开启一个线程来处理这个请求，对 URL 分析判断如果是 http 协议就按照 Web 方式来处理;
2. 调用浏览器内核中的对应方法，比如 WebView 中的 loadUrl 方法;
3. 通过DNS解析获取网址的IP地址，设置 UA 等信息发出第二个GET请求;
4. 进行HTTP协议会话，客户端发送报头(请求报头);
5. 进入到web服务器上的 Web Server，如 Apache、Tomcat、Node.JS 等服务器;
6. 进入部署好的后端应用，如 PHP、Java、JavaScript、Python 等，找到对应的请求处理;
7. 处理结束回馈报头，此处如果浏览器访问过，缓存上有对应资源，会与服务器最后修改时间对比，一致则返回304;
8. 浏览器开始下载html文档(响应报头，状态码200)，同时使用缓存;
9. 文档树建立，根据标记请求所需指定MIME类型的文件（比如css、js）,同时设置了cookie;
10. 页面开始渲染DOM，JS根据DOM API操作DOM,执行事件绑定等，页面显示完成。

**简洁版**

1. 浏览器根据请求的URL交给DNS域名解析，找到真实IP，向服务器发起请求；
2. 服务器交给后台处理完成后返回数据，浏览器接收文件（HTML、JS、CSS、图象等）；
3. 浏览器对加载到的资源（HTML、JS、CSS等）进行语法解析，建立相应的内部数据结构（如HTML的DOM）；
4. 载入解析到的资源文件，渲染页面，完成。
