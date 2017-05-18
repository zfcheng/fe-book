###1、行内元素和块元素
行内元素：水平分布；默认高度为内容高度；设置margin和padding值，盒模型会显示值，但只有左右有效；
块级元素：垂直分布；外边距合并；行内元素和块元素的互换方法

外边距合并：

* 外边距合并指的是，当两个垂直外边距相遇时，它们将形成一个外边距。
合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。
[w3school](http://www.w3school.com.cn/css/css_margin_collapsing.asp)
* 注释：只有普通文档流中块框的垂直外边距才会发生外边距合并。行内框、浮动框或绝对定位之间的外边距不会合并。

### 定位
* absolute　  生成绝对定位的元素，相对于 static 定位以外的第一个父元素进行定位。
* fixed 　　   生成绝对定位的元素，相对于浏览器窗口进行定位。
* relative　　生成相对定位的元素，相对于其正常位置进行定位。
* static　　   默认值。没有定位，元素出现在正常的流中
* inherit　　 规定应该从父元素继承 position 属性的值

### 盒子模型
* margin border padding content 
* 块元素不设置宽度，width = 100% ；

###css 选择器
* 1.id选择器（ # myid）
* 2.类选择器（.myclassname）
* 3.标签选择器（div, h1, p）
* 4.相邻选择器（h1 + p）
* 5.子选择器（ul < li）
* 6.后代选择器（li a）
* 7.通配符选择器（ * ）
* 8.属性选择器（a[rel = "external"]）
* 9.伪类选择器（a: hover, li: nth - child）

### 继承
* 可继承：font-size font-family color
* 不可继承 ：border padding margin width height

### box-sizing常用的属性有哪些？分别有什么作用？
* box-sizing: content-box|border-box|inherit;


### html5有哪些新特性？如何处理HTML5新标签的浏览器兼容问题？如何区分 HTML 和 HTML5？
* HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。

(1)绘画 canvas;

(2)用于媒介回放的 video 和 audio 元素;

(3)本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;

(4)sessionStorage 的数据在浏览器关闭后自动删除;

(5)语意化更好的内容元素，比如 article、footer、header、nav、section;

(6)表单控件，calendar、date、time、email、url、search;

(7)新的技术webworker, websocket, Geolocation;

IE8/IE7/IE6支持通过document.createElement方法产生的标签，可以利用这一特性让这些浏览器支持HTML5新标签，浏览器支持新标签后，还需要添加标签默认的样式。当然也可以直接使用成熟的框架、比如html5shim;

```
<!--[if lt IE 9]>
<script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
<![endif]-->
```

### 简述一下你对HTML语义化的理解？
* 用正确的标签做正确的事情。
* html语义化让页面的内容结构化，结构更清晰，便于对浏览器、搜索引擎解析;
* 即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的;
* 搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，利于SEO;
* 使阅读源代码的人对网站更容易将网站分块

### a：img的alt与title有何异同？b：strong与em的异同？
* strong:粗体强调标签，强调，表示内容的重要性
* em:斜体强调标签，更强烈强调，表示内容的强调点

### 简述一下src与href的区别
* src用于替换当前元素，href用于在当前文档和引用资源之间确立联系
* src是source的缩写，指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置； 当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕.
* href是Hypertext Reference的缩写，指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接; 并行下载资源并且不会停止对当前文档的处理

### 知道的网页制作会用到的图片格式有哪些？
* png-8，png-24，jpeg，gif，svg。
* Webp,Apng
* webp 支持情况

### 知道微格式吗？
* 微格式，microformats，它是一种利用HTML的class属性来对网页添加附加信息的方法，是一种开放的数据格式。
* 微格式是一种网络技术，用于将传统网页中的标签转化成元数据（描述数据的数据）以供机器和人阅读和使用。

### 在css/js代码上线之后开发人员经常会优化性能，从用户刷新网页开始，一次js请求一般情况下有哪些地方会有缓存处理？
* dns缓存，cdn缓存，浏览器缓存，服务器缓存。
