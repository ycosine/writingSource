零零散散搜索网上的知识感觉不太满意，感觉想通过自己写一点。
然后我发现有篇总结的不错的，所以下面的自己写的就比较姜

这个面试点主要考察你对DOM的事件机制的熟悉程度，以冒泡和捕获来作为切入点

参考： [javascript:深入理解事件流](https://segmentfault.com/a/1190000003497939)

[DOm事件流的三个阶段](https://segmentfault.com/a/1190000004463384)

# 定义：
- 1.事件流描述的是从页面中接收事件的顺序,也可理解为事件在页面中传播的顺序。
- 2.事件就是用户或浏览器自身执行的某种动作。诸如click(点击)、load(加载)、mouseover(鼠标悬停)。
- 3.事件处理程序响应某个事件的函数就叫事件处理程序(或事件侦听器)。

>'DOM2级事件'定义了两个方法，用于处理指定和删除事件处理程序的操作：addEventListener()和removeEventListener()。所有DOM节点中都包含这两个方法，并且它们都接收3个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。当这个布尔值为true时，表示在捕获阶段调用事件处理程序；若果是false，表示在冒泡阶段调用事件处理程序。

## 冒泡与捕获
> 不知道为什么这个东西我系统的接触非常少，以至于面试闻起来我答得方向完全不对。好吧不应该用方向这个词，是答的不对~~~在正常的框架事件模型中，一般事件是作为一种通讯方式以订阅和监听的方式来编写，其中DOM事件或者其他事件，比较常用的应该是 广播boardcast 以及提交分发 emit。这些都是经过封装的方法。而在JavaScript中，事件的设计获是经历了一段时间的发展和变化而的来的。
// 后来我才想起来这他妈其实是因为没有引导到浏览器DOM事件上，我对原生接触的面太少了。 W3C事件模型

## 事件冒泡 (dubbed  bubbling)

IE的事件流叫事件冒泡，即事件开始时由最具体的元素(文档中嵌套层次最深的节点)接收，然后逐级向上传播到较为不具体的节点。


我猜想的设计目的：冒泡设计的模型就像是责任链模式，可以集中处理多种操作，避免有成千上万的子元素要处理，添加如此多的处理事件



在一个对象中触发某类事件(例如onlick事件),**如果此对象定义了此事件的处理程序,那么此事件就会调用这个处理程序**

如果没有,那么这个事件会向这个对象的父级对象传播,从里到外直到他被处理(父级对象所有同类事件都被激活),或者它到达了对象层次的最顶层,即是document对象




## 事件捕获(event  capturing)
> 我真的日了这个翻译或者是什么鬼,捕获听起来像是事件监听的情况,至少我一开始是这样理解的。

Netscape团队提出的另一种事件流叫事件捕获，事件捕获的思想是不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。

（1） IE 从里到外的冒泡型事件
（2） Netscape4.0 从外到里的 捕获型事件
（3） DOM 事件流，先从外到里，再从里外回到原点的事件捕获

### 注意

不是所有的事件都能冒泡
1.blur,focus,load,unload 就不会冒泡
仔细想一想前面两个可以理解，后面两个我都不知道是干嘛的
[load]=>>(当一个资源及其依赖资源已完成加载时，将触发load事件。)

### 阻止事件冒泡

``` javasciprt
button.addEventListener('click', function(event) {
  // event为事件对象
  console.log('1. You click Button');
  event.stopPropagation();
  console.log('Stop Propagation!');
}, false);
```

个人感觉
捕获更像在搜索
冒泡更像在通知