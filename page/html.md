
## HTML
#### Doctype作用？标准模式与兼容模式各有什么区别?


`<!DOCTYPE>`声明位于HTML文档中的第一行，处于 `<html>` 标签之前。告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。

标准模式的排版 和JS运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示,模拟老式浏览器的行为以防止站点无法工作。

#### 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？

首先：CSS规范规定，每个元素都有`display`属性，确定该元素的类型，每个元素都有默认的`display`值，如div的display默认值为“block”，则为“块级”元素；span默认`display`属性值为`inline`，是“行内”元素。

- 行内元素有：`a b span img input select strong`（强调的语气）
- 块级元素有：`div ul ol li dl dt dd h1 h2 h3 h4…p`

- 常见的空元素：
`<br> <hr> <img> <input> <link> <meta>`
鲜为人知的是：
`<area> <base> <col> <command> <embed> <keygen> <param> <source> <track> <wbr>`

!> 不同浏览器（版本）、HTML4（5）、CSS2等实际略有差异
参考: http://stackoverflow.com/questions/6867254/browsers-default-css-for-html-elements



#### 页面导入样式时，使用link和@import有什么区别？


- link属于`XHTML`标签，除了加载CSS外，还能用于定义RSS, 定义rel连接属性等作用；而`@import`是CSS提供的，只能用于加载CSS;

- 页面被加载的时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载;

- `import`是CSS2.1 提出的，只在IE5以上才能被识别，而link是XHTML标签，无兼容问题;


#### 介绍一下你对浏览器内核的理解？

主要分成两部分：渲染引擎`(layout engineer或Rendering Engine)`和JS引擎。

- 渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入CSS等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。

- JS引擎则：解析和执行`javascript`来实现网页的动态效果。

最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。

#### 常见的浏览器内核有哪些？

- Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等。[又称MSHTML]
- Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等
- Presto内核：Opera7及以上。      [Opera内核原为：Presto，现为：Blink;]
- Webkit内核：Safari,Chrome等。   [ Chrome的：Blink（WebKit的分支）]

详细文章：[浏览器内核的解析和对比](http://www.cnblogs.com/fullhouse/archive/2011/12/19/2293455.html)



#### **HTML5**有哪些新特性、移除了那些元素？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？

!> HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。

- 绘画 `canvas`;
- 用于媒介回放的 video 和 audio 元素;
- 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
- sessionStorage 的数据在浏览器关闭后自动删除;
- 语意化更好的内容元素，比如 article、footer、header、nav、section;
- 表单控件，calendar、date、time、email、url、search;
- 新的技术webworker, websocket, Geolocation;

**移除的元素**：

- 纯表现的元素：`basefont，big，center，font, s，strike，tt，u`
- 对可用性产生负面影响的元素：`frame，frameset，noframes`

**支持HTML5新标签**：

- IE8/IE7/IE6支持通过`document.createElement`方法产生的标签，
- 可以利用这一特性让这些浏览器支持HTML5新标签，
- 浏览器支持新标签后，还需要添加标签默认的样式。

 当然也可以直接使用成熟的框架、比如`html5shim`;
 <!--[if lt IE 9]>
	<script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
 <![endif]-->

!> 如何区分HTML5： DOCTYPE声明\新增的结构元素\功能元素


#### 简述一下你对HTML语义化的理解？

- 用正确的标签做正确的事情。
- html语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎解析;
- 即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的;
- 搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，利于SEO;
- 使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

#### 请描述一下 cookies，sessionStorage 和 localStorage 的区别？

- cookie是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）。
- cookie数据始终在同源的http请求中携带（即使不需要），记会在浏览器和服务器间来回传递。
- sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。

**存储大小：**

- cookie数据大小不能超过4k。
- sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。

**有期时间：**

- localStorage    存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
- sessionStorage  数据在当前浏览器窗口关闭后自动删除。

- cookie          设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭

#### iframe有那些缺点？

* iframe会阻塞主页面的Onload事件；
* 搜索引擎的检索程序无法解读这种页面，不利于SEO;

* iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。

使用iframe之前需要考虑这两个缺点。如果需要使用iframe，最好是通过javascript
动态给iframe添加src属性值，这样可以绕开以上两个问题。

#### Label的作用是什么？是怎么用的？

label标签来定义表单控制间的关系,当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。
```html
	<label for="Name">Number:</label>
	<input type=“text“name="Name" id="Name"/>

	<label>Date:<input type="text" name="B"/></label>
```
#### 如何实现浏览器内多个标签页之间的通信? (阿里)

- WebSocket、SharedWorker；
- 也可以调用localstorge、cookies等本地存储方式；

#### title与h1的区别、b与strong的区别、i与em的区别？


- title属性没有明确意义只表示是个标题，H1则表示层次明确的标题，对页面信息的抓取也有很大的影响；

- strong是标明重点内容，有语气加强的含义，使用阅读设备阅读网络时：<strong>会重读，而<B>是展示强调内容。

- i内容展示为斜体，em表示强调的文本；

- Physical Style Elements -- 自然样式标签
- b, i, u, s, pre
- Semantic Style Elements -- 语义样式标签
- strong, em, ins, del, code
- 应该准确使用语义样式标签, 但不能滥用, 如果不能确定时首选使用自然样式标签。

## CSS
#### 介绍一下标准的CSS的盒子模型？低版本IE的盒子模型有什么不同的？

- 有两种， IE 盒子模型、W3C 盒子模型；
- 盒模型： 内容(content)、填充(padding)、边界(margin)、 边框(border)；
- 区  别： IE的content部分把 border 和 padding计算了进去;



#### CSS选择符有哪些？哪些属性可以继承？

1. id选择器（ # myid）

2. 类选择器（.myclassname）

3. 标签选择器（div, h1, p）

4. 相邻选择器（h1 + p）

5. 子选择器（ul > li）

6. 后代选择器（li a）

7. 通配符选择器（ * ）

8. 属性选择器（a[rel = "external"]）

9. 伪类选择器（a:hover, li:nth-child）

*   可继承的样式： font-size font-family color, UL LI DL DD DT;

*   不可继承的样式：border padding margin width height ;



#### CSS优先级算法如何计算？

*   优先级就近原则，同权重情况下样式定义最近者为准;
*   载入样式以最后载入的定位为准;

!> 优先级为:
同权重: 内联样式表（标签内部）> 嵌入样式表（当前文件中）> 外部样式表（外部文件中）。
!important >  id > class > tag
important 比 内联优先级高

#### CSS3新增伪类有那些？

举例：

- p:first-of-type	选择属于其父元素的首个 `<p>` 元素的每个 `<p>` 元素。

- p:last-of-type	选择属于其父元素的最后 `<p>` 元素的每个 `<p>` 元素。

- p:only-of-type	选择属于其父元素唯一的 `<p>` 元素的每个 `<p>` 元素。

- p:only-child		选择属于其父元素的唯一子元素的每个 `<p>` 元素。

- p:nth-child(2)	选择属于其父元素的第二个子元素的每个 `<p>` 元素。


* ::after			在元素之前添加内容,也可以用来做清除浮动。
* ::before			在元素之后添加内容
* :enabled  		
* :disabled 		控制表单控件的禁用状态。
* :checked        单选框或复选框被选中。

#### 如何居中div？


*  水平居中：给div设置一个宽度，然后添加margin:0 auto属性
```css
div{
		width:200px;
		margin:0 auto;
}
```
*  让绝对定位的div居中
```css
div {
		position: absolute;
		width: 300px;
		height: 300px;
		margin: auto;
		top: 0;
		left: 0;
		bottom: 0;
		right: 0;
		background-color: pink;	/* 方便看效果 */
}
```
*  水平垂直居中一

确定容器的宽高 宽500 高 300 的层
设置层的外边距
```css
div {
		position: relative;		/* 相对定位或绝对定位均可 */
		width:500px;
		height:300px;
		top: 50%;
		left: 50%;
		margin: -150px 0 0 -250px;     	/* 外边距为自身宽高的一半 */
		background-color: pink;	 	/* 方便看效果 */

}
```
*  水平垂直居中二

未知容器的宽高，利用 `transform` 属性
```css
div {
		position: absolute;		/* 相对定位或绝对定位均可 */
		width:500px;
		height:300px;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		background-color: pink;	 	/* 方便看效果 */

}
```
*  水平垂直居中三

利用 flex 布局
实际使用时应考虑兼容性
```css
.container {
		display: flex;
		align-items: center; 		/* 垂直居中 */
		justify-content: center;	/* 水平居中 */

}
.container div {
		width: 100px;
		height: 100px;
		background-color: pink;		/* 方便看效果 */
 }  

```
#### display有哪些值？说明他们的作用。

- `block`       	块类型。默认宽度为父元素宽度，可设置宽高，换行显示。
- `none`        	缺省值。象行内元素类型一样显示。
- `inline`      	行内元素类型。默认宽度为内容宽度，不可设置宽高，同行显示。
- `inline-block`  默认宽度为内容宽度，可以设置宽高，同行显示。
- `list-item`   	象块类型元素一样显示，并添加样式列表标记。
- `table`       	此元素会作为块级表格来显示。
- `inherit`     	规定应该从父元素继承 display 属性的值。


#### position的值relative和absolute定位原点是？

- `absolute`生成绝对定位的元素，相对于值不为 static的第一个父元素进行定位。
- `fixed` （老IE不支持）生成绝对定位的元素，相对于浏览器窗口进行定位。
- `relative`生成相对定位的元素，相对于其正常位置进行定位。
- `static`默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right z-index 声明）。
- `inherit`规定从父元素继承 position 属性的值。

#### CSS3有哪些新特性？

* 新增各种CSS选择器	（: not(.input)：所有 class 不是“input”的节点）
* 圆角		    （border-radius:8px）
* 多列布局	    （multi-column layout）
* 阴影和反射	（Shadow\Reflect）
* 文字特效		（text-shadow、）
* 文字渲染		（Text-decoration）
* 线性渐变		（gradient）
* 旋转		 	（transform）
* 缩放,定位,倾斜,动画,多背景
* 例如: `transform:\scale(0.85,0.90)\ translate(0px,-30px)\ skew(-9deg,0deg)\Animation:`

#### 请解释一下CSS3的Flexbox（弹性盒布局模型）,以及适用场景？

> 一个用于页面布局的全新CSS3功能，Flexbox可以把列表放在同一个方向（从上到下排列，从左到右），并让列表能延伸到占用可用的空间。
较为复杂的布局还可以通过嵌套一个伸缩容器（flex container）来实现。

采用Flex布局的元素，称为Flex容器（flex container），简称"容器"。
它的所有子元素自动成为容器成员，称为Flex项目（flex item），简称"项目"。
常规布局是基于块和内联流方向，而Flex布局是基于flex-flow流可以很方便的用来做局中，能对不同屏幕大小自适应。
在布局上有了比以前更加灵活的空间。

具体：http://www.w3cplus.com/css3/flexbox-basics.html

#### 用纯CSS创建一个三角形的原理是什么？

把上、左、右三条边隐藏掉（颜色设为 `transparent`）
```css
demo {
		width: 0;
		height: 0;
		border-width: 20px;
		border-style: solid;
		border-color: transparent transparent red transparent;
}
```

#### 经常遇到的浏览器的兼容性有哪些？原因，解决方法是什么，常用hack的技巧 ？

* png24位的图片在iE6浏览器上出现背景，解决方案是做成PNG8.

* 浏览器默认的margin和padding不同。解决方案是加一个全局的*{margin:0;padding:0;}来统一。

* IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。

* 巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。

```css
.bb{
		background-color:red;/*所有识别*/
		background-color:#00deff\9; /*IE6、7、8识别*/
		+background-color:#a200ff;/*IE6、7识别*/
		_background-color:#1e0bd1;/*IE6识别*/
}
```

*  IE下,可以使用获取常规属性的方法来获取自定义属性,
也可以使用getAttribute()获取自定义属性;
Firefox下,只能使用getAttribute()获取自定义属性。
解决方法:统一通过getAttribute()获取自定义属性。

*  IE下,even对象有x,y属性,但是没有pageX,pageY属性;
Firefox下,event对象有pageX,pageY属性,但是没有x,y属性。

*  解决方法：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。

*  Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,
可通过加入 CSS 属性 ``-webkit-text-size-adjust: none;`` 解决。

*  超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了解决方法是改变CSS属性的排列顺序:
`L-V-H-A :  a:link {} a:visited {} a:hover {} a:active {}`

#### 为什么要初始化CSS样式。

- 因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。

- 当然，初始化样式会对SEO有一定的影响，但鱼和熊掌不可兼得，但力求影响最小的情况下初始化。

最简单的初始化方法： `* {padding: 0; margin: 0;}` （强烈不建议）

> 可以采用淘宝的样式初始化代码：

```css
body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin:0; padding:0; }
body, button, input, select, textarea { font:12px/1.5tahoma, arial, \5b8b\4f53; }
h1, h2, h3, h4, h5, h6{ font-size:100%; }
address, cite, dfn, em, var { font-style:normal; }
code, kbd, pre, samp { font-family:couriernew, courier, monospace; }
small{ font-size:12px; }
ul, ol { list-style:none; }
a { text-decoration:none; }
a:hover { text-decoration:underline; }
sup { vertical-align:text-top; }
sub{ vertical-align:text-bottom; }
legend { color:#000; }
fieldset, img { border:0; }
button, input, select, textarea { font-size:100%; }
table { border-collapse:collapse; border-spacing:0; }
```


#### CSS里的visibility属性有个collapse属性值是干嘛用的？在不同浏览器下以后什么区别？

* 对于普通元素visibility:collapse;会将元素完全隐藏,不占据页面布局空间,与display:none;表现相同.
* 如果目标元素为table,visibility:collapse;将table隐藏,但是会占据页面布局空间.
* 仅在Firefox下起作用,IE会显示元素,Chrome会将元素隐藏,但是占据空间.

#### position跟display、margin collapse、overflow、float这些特性相互叠加后会怎么样？

- 如果元素的`display为none`,那么元素不被渲染,position,float不起作用
- 如果元素拥有`position:absolute`;或者`position:fixed`;属性那么元素将为绝对定位,float不起作用.
- 如果元素float属性不是none,元素会脱离文档流,根据float属性值来显示.有浮动,绝对定位,inline-block属性的元素,margin不会和垂直方向上的其他元素margin折叠.

#### css定义的权重

以下是权重的规则：标签的权重为1，class的权重为10，id的权重为100，以下例子是演示各种定义的权重值：
```css
/*权重为1*/
div{
}
/*权重为10*/
.class1{
}
/*权重为100*/
#id1{
}
/*权重为100+1=101*/
#id1 div{
}
/*权重为10+1=11*/
.class1 div{
}
/*权重为10+10+1=21*/
.class1 .class2 div{
}
```
如果权重相同，则最后定义的样式会起作用，但是应该避免这种情况出现


#### 请解释一下为什么需要清除浮动？清除浮动的方式

!> 清除浮动是为了清除使用浮动元素产生的影响。浮动的元素，高度会塌陷，而高度的塌陷使我们页面后面的布局不能正常显示。

1. 父级div定义height；
2. 父级div 也一起浮动；
3. 常规的使用一个class；
```css
.clearfix::before, .clearfix::after {
content: " ";
display: table;
}
.clearfix::after {
clear: both;
}
.clearfix {
*zoom: 1;
}
```

#### 什么是外边距合并？

外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。
合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。
w3school介绍网址： http://www.w3school.com.cn/css/css_margin_collapsing.asp

#### 移动端的布局用过媒体查询吗？


假设你现在正用一台显示设备来阅读这篇文章，同时你也想把它投影到屏幕上，或者打印出来，
而显示设备、屏幕投影和打印等这些媒介都有自己的特点，CSS就是为文档提供在不同媒介上展示的适配方法

<!-- link元素中的CSS媒体查询 -->
当媒体查询为真时，相关的样式表或样式规则会按照正常的级联规被应用。
当媒体查询返回假， <link> 标签上带有媒体查询的样式表 仍将被下载 （只不过不会被应用）。
```html5
<link rel="stylesheet" media="(max-width: 800px)" href="example.css" />
```
<!-- 样式表中的CSS媒体查询 -->
包含了一个媒体类型和至少一个使用 宽度、高度和颜色等媒体属性来限制样式表范围的表达式。
CSS3加入的媒体查询使得无需修改内容便可以使样式应用于某些特定的设备范围。
```
<style>
@media (min-width: 700px) and (orientation: landscape){
.sidebar {
display: none;
}
}
</style>
```

#### CSS优化、提高性能的方法有哪些？

- 关键选择器（key selector）。选择器的最后面的部分为关键选择器（即用来匹配目标元素的部分）；
- 如果规则拥有 ID 选择器作为其关键选择器，则不要为规则增加标签。过滤掉无关的规则（这样样式系统就不会浪费时间去匹配它们了）；
- 提取项目的通用公有样式，增强可复用性，按模块编写组件；增强项目的协同开发性、可维护性和可扩展性;
- 使用预处理工具或构建工具（gulp对css进行语法检查、自动补前缀、打包压缩、自动优雅降级）；


#### margin和padding分别适合什么场景使用？

- `margin`是用来隔开元素与元素的间距；padding是用来隔开元素与内容的间隔。
- `margin`用于布局分开元素使元素与元素互不相干；
- `padding`用于元素与内容之间的间隔，让内容（文字）与（包裹）元素之间有一定的间隔


#### 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？

#### ::before 和 :after中双冒号和单冒号 有什么区别？解释一下这2个伪元素的作用。

- 单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素。（伪元素由双冒号和伪元素名称组成）
- 双冒号是在当前规范中引入的，用于区分伪类和伪元素。不过浏览器需要同时支持旧的已经存在的伪元素写法，

#### 如何修改chrome记住密码后自动填充表单的黄色背景 ？

```css
input:-webkit-autofill, textarea:-webkit-autofill, select:-webkit-autofill {
		background-color: rgb(250, 255, 189); /* #FAFFBD; */
		background-image: none;
		color: rgb(0, 0, 0);
}
```

#### overflow: scroll时不能平滑滚动的问题怎么处理？


#### 什么是Cookie 隔离？（或者说：请求资源的时候不要让它带cookie怎么做）

如果静态文件都放在主域名下，那静态文件请求的时候都带有的cookie的数据提交给server的，非常浪费流量，
所以不如隔离开。

因为cookie有域的限制，因此不能跨域提交请求，故使用非主要域名的时候，请求头中就不会带有cookie数据，
这样可以降低请求头的大小，降低请求时间，从而达到降低整体请求延时的目的。

同时这种方式不会将cookie传入Web Server，也减少了Web Server对cookie的处理分析环节，
提高了webserver的http请求的解析速度。


#### style标签写在body后与body前有什么区别？

#### 什么是CSS 预处理器 / 后处理器？

- 预处理器例如：`LESS、Sass、Stylus`，用来预编译`Sass`或`less`，增强了css代码的复用性，
还有层级、mixin、变量、循环、函数等，具有很方便的UI组件模块化开发能力，极大的提高工作效率。

- 后处理器例如：`PostCSS`，通常被视为在完成的样式表中根据CSS规范处理CSS，让其更有效；目前最常做的
是给CSS属性添加浏览器私有前缀，实现跨浏览器兼容性的问题。


#### rem布局的优缺点
