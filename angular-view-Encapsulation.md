# Angular2 组件视图/样式封装机制

> 尽管css的意思是**层叠演示表**，但有时候我们并不需要"层叠"。既然angular采用了组件化的设计模式，那么
>我们能不能采用组件化的方式，为某个组件提供特定的局部（组件级别）个性样式而不影响到页面的其他部分，答案是肯定的。

### 1.标准html中样式的引入方式：
 1. 内联样式：
 
 <details>
 直接在元素标签内设置css
 <summary>
    <code><div style="background-color:red">内联样式</div></code>
 </summary>
 </details> 
 
 2. 标签演示：采用`style`标签元素设定，eg:`<style> .nav-bar{font:14px;}</style>`
 3. 链接引入方式
 4. 导入方式