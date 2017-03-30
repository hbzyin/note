# Angular 指令

**Angular的设计核心理念是数据绑定、组件化.** 请时刻牢记这句话！

按照惯例，先来剧情透露：

- angular指令种类
- angular内置ngif指令
- `<template>`标签
- `*ngIf`语法糖
- 学习自定义一个指令

### 1.angular指令种类
Angular的指令分为以下三种：
- 组件
- 属性指令
- 结构指令

① 组件
> Angular应用是由一个个的组件（component）构成的;组件是由html模板、组件类构成。
> html模板实现页面的展示内容，组件类用来控制视图的展示形式。每一个组件都以@Component装饰器函数开始，该函数接受一个元数据对象参数，
这个元素苏描述了html模板与组件类如何协同工作的。

②属性指令
> 属性指令用于改变元素的外观和行为。如内置的`ngClass`、`ngStyle`指令。

③结构指令

>结构指令通过添加或删除DOM元素来改变DOM布局。如内置的`ngIf`、`ngSwitch`、`ngFor`等指令。

***下面我们主要针对`ngIf`来谈一下angular的一部分优缺点。***

先看一个栗子：
```angular2html
<p *ngIf="true">
This information1 is displayed if condition is true.
</p>
<p *ngIf="!true">
Tihs information2 is deleted if condition is true.
</p>
```
打开浏览器及开发工具，效果如下;
![](sources/page1.png)
![](sources/code1.png)

我们看到dom树里面只有一个段落，也就是说第二个段落被*ngIf指令从DOM树种移除了，当然我们也可以通过设置元素节点css属性display:none将其隐藏。
为什么angular将其从DOM树种删除，而不是隐藏，我们先来看看两者之间的区别：

①元素隐藏：元素仍在页面DOM树里面存在，仍然实时监听着页面的事件，如果绑定了数据，angular会继续对其进行动态监测；
②元素删除：元素彻底从页面DOM树消失，不会对页面的事件、数据及渲染造成任何影响；

我们之前说过，angular设计的核心理念之一便是数据绑定，就像官网所说： 
> 最小化初始化的成本，并考虑把状态缓存在一个半生的服务中。

angular核心对数据进行自动检测；dom元素的操作、数据脏值检测，这两件事都是非常消耗cpu内存的，
angular吸取了angular1数据绑定的负面经验，采用了第一种方案。无疑这对于数据动态监听来说效率提高了很多，但仍不能说这是一个最好的实践方法。
作为一个开发者，在自定义新的指令时，我们同样面临着这种取舍，需要仔细考量添加元素、删除元素及销毁组件的成本和效率。