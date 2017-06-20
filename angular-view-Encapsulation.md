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
 
 ### 3. angular视图封装——shadow DOM
 
 > 场景1：开发angular项目时，假如我们在配置文件.angular.cli.json、组件内联/外联、标签内，多处都设置了同样的样式，页面改如何展示？
 
  让我们先来预测一下结果：
  a.加入三处引入的样式都没有采用`!important`,那么根据优先级，页面的样式也就是标签内嵌样式的结果；
  b.