# Angular2 组件视图/样式封装机制

> 尽管css的意思是**层叠样式表**，但有时候我们并不需要"层叠"。既然angular采用了组件化的设计模式，那么
>我们能不能采用组件化的方式，为某个组件提供特定的局部（组件级别）个性样式而不影响到页面的其他部分，答案是肯定的。

### 1.标准html中样式的引入方式：
 1. 内嵌样式：直接在元素标签内设置css,如下栗子：
    `<div style="background-color:red">内联样式</div>`
 2. 标签样式：采用`style`标签元素设定，如下栗子：
 ```angular2html
  <style> 
    .nav-bar{font-size:14px;}
  </style>`
  ```
 3. 链接引入样式:
     `<link rel="stylesheet" type="text/css" href="style.css">`
 4. 导入样式:
     ```angular2html
     <style>
          @import url(../xx/style.css);
     </style>
    ```
 ### 2.angular中样式引用方式：
 1. 全局样式引入
    1. 配置文件设置：.angular.cli.json文件中设置:`"apps":{
           "styles": ["scss/style.scss"],
           "scripts":[...]
          }` 
    2. 入口文件引入：index.html文件中：`<link href="assets/css/font-awesome.min.css" rel="stylesheet">`
    3. 入口文件样式块：`<style>.nav-bar{font-size:12px;}</style>`
 2. 组件级别引入：
    1. 组件内联：`styles:".nav-bar{font-size:16px;}`
    2. 组件外联：`styleUrls:['./session.component.scss']`
 3. 标签级别样式：`<div style="font-color:red"></div>`
 
 ### 3. shadow DOM
 
 ##### 3.1：开发angular项目时，假如我们在配置文件.angular.cli.json、组件内联/外联、标签内，多处都设置了同样的样式，页面改如何展示？
 
  让我们先来预测一下结果：
  a.假如三处引入的样式都没有采用`!important`,那么根据优先级，页面的样式也就是标签内嵌样式的结果；
  b.假如三处引入的样式具有javascript模式的变量作用域概念，那么页面的样式应该是最小子组件覆盖父层组件样式；
  c.假如三处引入样式具有样式重写效果，那么，将按照样式的定义先后顺序，最后定义的样式覆盖先定义的样式；
  
 > 令人兴奋的是，上面三种我们预测的效果，angular都有实现的技术：你所需要做的仅仅是在组件定义时加上一条元数据：`encapsulation:ViewEncapsulation.Emulate/Native/None`
 > 而这些神奇的功能效果，背后所支撑的技术就是目前组件化前端框架的基础：**Shadow Dom**.
 
 ##### 3.2 Shadow DOM
 什么是shadow dom技术？
 简单来说，就是浏览器标准中开放给开发者用来自定义 html标签元素的API,接口也极其简单：`Element.createShadowRoot()`;
 
 Shadow DOM允许开发者在页面的DOM树结构里面，插入自定义的DOM元素子树，DOM元素子树的内容、页面样式、javascript均与宿主DOM树相互独立.
 
 ***没错，这就是当今2017年前端最流行的组件化设计思想，得以实现的技术基础！！！***
 刨根问底，请用力戳破==>
 [MDN文档](https://developer.mozilla.org/zh-CN/docs/Web/Web_Components/%E5%BD%B1%E5%AD%90_DOM)、
 [参考文章](https://aotu.io/notes/2016/06/24/Shadow-DOM/index.html)。
 
 ### 4. angular视图封装 
  ——————`encapsulation:ViewEncapsulation.Emulate/Native/Native`
 