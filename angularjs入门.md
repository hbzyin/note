# Angularjs入门——(1-9章)

###### 声名：本系列所有内容都是angular2.0以下版本，如需要查看angular2.0及以上版本相关，请另寻出路。

1. angularJS是什么?
>AngularJS是一种采用MVC/MVVM模式设计的用于快速构建单页面应用SPA的JavaScript前端框架。开发者可以利用它将页面的一部分封装为一个应用，而不强迫整个页面都是使用AngularJS进行开发，甚至将页面的其他部分应用其他框架进行构建。angularJS的核心思想主要有4点：依赖注入、模块化、双向数据绑定、语义化标签。
>
> PS:angular2的核心包括6个方面：组件、模板、指令、服务、依赖注入、路由
2. angularJs的适用场景
> angularJS采用MVC设计模式，将所有数据都绑定在内部构建的全局数据模型对象$scope上，实现表现分离（即视图和逻辑的分离）； angularJS认为某个值可能会发生变化时，会运行自己的事件循环机制来检查这个值是否为“脏”。如果某个值在任意一次事件循环前后发生了变化，则认为是"脏"，这就是饱受诟病的脏检查机制，也是anguular能追踪和响应变化的原因所在；
>
>angularJS创建实时模板来替代视图，而不是像react一样将数据合并进模板之后更新视图，所以该框架不适应于频繁进行DOM操作的业务场景，如游戏、图形编辑器等；相反双向数据绑定，是的其更适应于构建CRUD频繁的应用场景，如管理系统、ERP等；
3. 核心思想——模块化
> 默认情况下，angularJS构建的应用中，所有数据及属性都绑定在內建全局命名空间对象$scope上，而angular采用了模块作为定义应用的主要方式，每个模块包含了定义具体功能的代码(可以理解为 指令、控制器、服务、数据模型、视图的一个容器)。开发大型应用时，通常会将复杂的业务功能分割为不同的模块，创建多个模块来承载业务逻辑，同时保证应用可以按需以任意顺序加载各个模块的代码。
>
> 模块的定义如下：
```
angular.module(name,[require1,require2,...]);
//参数1 name:模块的名称，类型为字符串变量
//参数2 require1 ... 所依赖模块的名称
```

4. 內建对象$scope——angularJS的作用域
> 作用域是代码执行的上下文，angularJS中的作用域同样是angularJS应用的**核心**基础，也是应用状态的基础。angularJS的作用域$scope是和应用数据模型相关联的，是定义应用业务逻辑、控制器方法、视图属性的对象/地方。作用域($scope)作为视图和HTML之间的桥梁、视图和控制器之间的胶水，并不负责处理和操作数据，通常处理操作数据在服务中进行，后续会详细讲解。
>
> angularJS的应用负责将包含html标准元素、angularJS自定义元素的HTML进行渲染，并将渲染后的HTML交给浏览器来进行显示；在应用将视图渲染并呈现给用户之前，视图中的模板会和作用域进行连接，然后应用会对DOM进行设置以便将属性变化通知给angularJS.
>
> angularJS的指令会创建孤立作用域。

  4.1. angularJS中模板可应用的标记包含以下几类：
    - 指令：将DOM元素增强为可复用DOM组件的属性或元素；
    - 值绑定：模板语法`{{}}`可以将表达式绑定到视图；
    - 过滤器：可以在视图中使用的函数，用来进行格式化
    - 表单控件：用来检验用户输入的控件

  4.2. $scope的生命周期

  > angular会监听应用中所有的数据模型对象，当监听的事件在浏览器中发生时，如`ng-model`属性绑定的输入字段、`ng-click`属性的元素被点击时，angular事件循环都会触发，执行脏检查，这个事件将爱angularJS中执行上下文处理。$scope的生命周期分为以下几个阶段（angularJS V1.2.x）:
  - 创建：创建控制器、指令时，angularJS会用$injector创建一个作用域，并在新建的控制器或指令运行时将作用域传进去；
  - 链接：应用开始运行时，所有的$scope对象都会**附加**或**链接**到视图中，所有创建$scope对象的函数也会将自身附加到视图中，这些作用域会注册当应用上下文发生变化是需要运行的`$watch`函数，从而在适当时机触发事件循环；
  - 更新：当事件循环运行时，它通常执行在顶层的`$scope`(`$rootScope`)对象上,每个子作用域会执行自己的脏值检测；每个监控函数都会检查变化，如果检测到任意变化，$scope都会触发指定的回调函数；
  - 销毁：当一个$scope在视图中不再需要时，这个作用域会清理并销毁自己，此外开发者可以使用$scope上的`$destory()`方法来手动清理不需要的作用域($scope)；

  4.3 脏检查机制 `$watch`、`$apply`、`$digest`

  > 浏览器更新页面内容是通过事件触发的，浏览器一直在等待事件，如用户的输入、事件队列等；当有事件发生时，事件的回调函数就会在javascript解释器里执行，然后允许用户在回调函数里进行各种操作。angular扩展了这个事件循环，生成一个`angular context`（即$scope）的执行环境。
  >
  - 数据绑定：当用户在UI/HTML界面绑定一个数据模型或者属性的时候，就会在`$watch`队列里插入一条$watch，$watch就是用来检测它监视的model的变化，同时记录变更前后的数据；没有被绑定到UI界面的数据模型不会插入$watch队列；
  - 脏检查事件的触发：绑定在UI视图上的数据模型，angularJS会自动的调用`$apply`服务，将视图层面的数据变化更新到数据模型上(即html数据->`$scope`对象)；但此时仅实现了视图到数据模型的单向数据流；
  - $digest循环：当$watch监听的数据模型发生变化，并且调用了$apply服务时，$apply会调用`$digest`事件循环，逐一检查每个数据模型、属性，当检测到数据模型发生变化是，会将数据模型更新到视图界面，此时完成数据模型到视图的反向数据流；当$digest检查完所有的$watch队列时，发现所有数据都没有变化，angular会自动触发下一次检查，如果循环次数超过10且每次都没有数据变化，他会跑出一个异常，防止无线循环，结束`$digest`循环，DOM元素停止更新

  ```
  $watch(name,function(newVal,oldVal){},bollean);
    // 参数 name:需要监听的属性/属性名，字符串
    // 参数 newVal、oldVal： 监听对象属性变化后、变化前的值,泛型
    // 参数 boolean：表示$watch比较的是对象值，而不是引用
  ```

5. 核心概念——控制器
> angularJS中的控制器是一个函数(亦即一个类)，可以将与一个独立视图相关的业务逻辑封装在一个独立的容器中；控制器主要用来存储数据模型，而执行DOM操作、格式化、数据操作等状态维护操作通常通过依赖注入相关的指令、服务来操作；angularJS中的控制器可以进行嵌套，除了指令内部创建的孤立作用域外，所有控制器创建时传入的作用域都会通过原型来继承，即可以访问父级作用域。
>
> 控制器的创建方式有如下2种：
```
// 方法1 控制器在AngularJS全局作用域中命名
function Controller($scope,$otherDep){};
// 方法2 控制器命名在angularJS的模块modulA中创建
angular.module('moduleA',[]).controller('controller1',function($scope,$otherDep){});
```
6. 表达式
> anhgularJS采用`{{}}`将一个变量绑定到$scope上的本质就是一个表达式：`{{expression}}`，表达式和`eval(javascript)`非常相似，但是由AngularJs来处理。当用`$watch`表达式时，angularJS会通过`$parse`这个内部服务访问当前的作用域进而进行表达式的运算。
>
> 通常angularJS会在运行`$digest`循环的过程中自动解析表达式，开发者也可以通过调用`$parse（expression）`这个内部服务来手动解析表达式。$parse的作用是讲一个AnglarJS表达式转换成一个函数；
>
> 同样，angularJS可以让开发者拥有手动运行编译模板的能力，在对象中注入`$interpolate`服务后，插值允许基于作用域上的某个条件实时更新文本字符串
```
// 1. 插值表达式解析：$parser(expression)
var $scope.expression='something'
var parseFun=$parser(expression); //expression：需要被编译的angularJS语句；
var res=parseFun;       // 返回值为一个函数fn(context,localContext)
cosnole.dir(res)        //   context需要解析的语句的作用域;
                        // localContext 关于context中变量的本地变量，对于覆盖context中的变量个非常有用
console.dir(res.assign); // 返回函数的方法assign()
```
```
// 2.插值字符串解析：$interpolate(context)
var tmp = $interpolate('Publish by {{name}} on {{date}}'); //返回值为一个函数  fn(context),输入参数为上下文环境
var data1 = {name: 'Mike',date: '2014-1-1'};
var data2 = {name: 'Karen',date: '2014-1-2'};
var str1 = tmp(data1);
var str2 = tmp(data2);
console.dir(tmp);  //
console.log(str1); // Publish by Mike on 2014-1-1
console.log(str2); // Publish by Karen on 2014-1-2
```
7. 过滤器&表单验证
> 过滤器本质上是将输入的内容作为参数的一个函数，类似于JS原生的数组/对象的方法,用来格式化需要展示给用户的数据。angularJS内置了9种过滤器，并且用户可以自定义过滤器。在html中绑定的插值内通过`|`符号来调用相关的过滤器;过滤器传入的参数用`:`分割，多个过滤器可以同时使用，如：`{{name | uppercase | limitTo:2}}`(输出：NA);
  - `upppercase` ：可以将字符串全部转化为大写形式：`{{"Origin Text" | upppercase}}`，输出：ORIGIN TEXT
  - `lowercase`  : 可以将字符串全部转换为小写形式：`{{"Origin Text" | lowercase}}` ,输出：origin text
  - `currency`   : 将一个数值转换为货币形式，如：`{{123 | currency}}`,输出：￥123
  - `date`：将日期格式化成需要的格式，如：`{{ new Date() | date："yyyy-MM-DD" }}`，输出:2017-11-03
  - `number`:将数字格式化成文本，如：`{{ 1234567 | number}}`,输出为：1,234,567
  - `json`：将一个JSON或JavaScript对象装换成字符串,如：`{{ {"name":'Aya',"age":23} | json }}`,输出：{"name":"Aya","age":23}
  - `orderBy`:用表达式对指定的数组进行排序，如：`{{ [{'name':'Json','name':'Lilly'}] | oderBy:'name'}}`,输出：[{'name':'Lilly'},{'name':'Json'}]
  - `limitTo`: 截取字符串/数组的部分字符/元素作为输出，如：`{{"start"|limitTo:2}}` 、`{{[1,2,3]|limitTo:-2}}`；
  - `filter`:从给定的数组中选取符合条件的子集进行输出，如:`{{['at','name','sst']|filter:'a'}}`,输出:['at','name'];filter传入的参数可以为①String:返回包含指定字符的元素集；②对象：返回包含指定对象同名属性中属性值的子元素集合；③函数：返回满足函数条件的元素集；
  - 自定义过滤器：如下例：
  ```
  angular.module('app',[]).filter('newFilter',function(){
    return function(input){
      if(input){
        return input[0].toUpperCase()+input.slice(1);
      }
    }
  })
<!-- html -->
{{'Something For Test'| lowercase | newFilter }} // 输出：Something for test
```
8. 指令
> 浏览器会渲染html的内容、样式、行为，这是web功能强大的基础；angularJS扩展了具有自定义功能的html标签、属性、类，声名指令的本质就是在html中通过元素/标签、属性、类、注释来添加功能；
  - 指令命名：采用驼峰命名
  - 指令引用：蛇形命名
  - 指令应用方式：标签(E)、属性(A)、类(C)、注释(M)
  - 示例
  ```
  angular.module('myApp',[])
  .directive('myDirective',function(){
   return {
       restrict:'AECM',
       replace:true,   //是否完全移除自定义标签
       template:`<p href="{{myUrl}}" ng-click="eventFn()">{{myName}} my age is:{{age}}</p>`,
       scope:{
         myUrl:'@', //
         myName:'@',//将外部传入变量(myName) 复制一份赋值给指令内部同名变量(myName)
         age:'=myAge',//将外部传入变量(myAge) 复制一份赋值指令内部变量(age)
      // eventFn:'&'  //将内部函数eventFn与外部传入事件函数eventFn进行绑定；
       }
     }
  })
  <!-- html -->
  <my-directive my-url="a.cm" my-name="this is the binding text." my-age='13' eventFn=alert(1)><my-directive>
  <!-- <div class="my-dir"></div> -->
  <!-- <div my-dir></div> -->
  <!-- directive:my-dir -->
  ```
9. 内置指令
> angularJS提供了一系列的内置指令，其中一些指令重载了原生的html元素，如`<a>`和`<form>`标签，这些重载的标签扩展了一系列高级的功能，但在html中使用时不一定能明确看出是否在使用指令；其他的内置指令通常以`ng`为前缀作为命名空间，用户也可以自定义一些列的指令，为了便于和内置指令区分，官方建议不要使用`ng`作为前缀，以避免指令污染；
> 内置指令根据其是否使用作用域分为基础属性指令、使用自作用于的指令两大类，除事件绑定类指令常用的共25个内置指令：
  - 属性指令(布尔)：4个(ng-disabled、ng-checked、ng-readonly、ng-selected)，根据html标准定义，布尔属性代表true或false；当这个值出现时，这个值就是ture,如果未出现，这个属性就是false;
  - 属性指令(类布尔)：2个(ng-href、ng-src)，不是html标准的布尔属性，但与布尔类型属性行为类似；
  - 作用域指令(构建类)：2个(ng-app、ng-controlller)，他们会修改嵌套在其内部的指令的作用域；
  - 作用域指令(视图类)：2个(ng-include、ng-view)，主要用来加载、编译应用外部html片段，或者为内部html设置路由管理的视图位置；
  - 作用域指令(表单类)：2个(ng-form、ng-selecet)，主要用来设置与表单输入相关指令；
  -
  - 作用域指令(样式类)：4个+(ng-class、ng-attr-(suffix)、ng-show、ng-hide..),主要用来设置标签元素的样式类名`class`或属性；
  - 作用域指令(逻辑类)：3个(ng-switch、ng-repeat、ng-if)主要通过逻辑处理来进行页面视图的输出显示；
  - 作用域指令(数据绑定类)：6个(ng-init、ng-model、{{}}、ng-cloak、ng-bind、ng-bind-template)：主要用来对html页面视图与数据模型进行绑定；
  - 作用域指令(事件绑定)：(ng-click、ng-submit、ng-dbclick、ng-change、ng-mouseover、ng-mouseout、ng-mouseenter、ng-mouseleave...)
10.
