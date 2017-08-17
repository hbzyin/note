## 文件操作

#### 1. Html5 二进制数据操作接口

>Javascript中对二进制数据进行操作的API

>1.`str.charCodeAt(index)`:获取字符串str中某个字符的Unicode编码；
>
>2.`window.Blob`：javascript中代表二进制数据的基本对象，html 5中新增对二进制数据进行处理API;
>一个Blob对象就是一个包含有只读原始数据的类文件对象。
Blob对象中的数据并不一定得是JavaScript中的原生形式。
File接口基于Blob，继承了Blob的功能,并且扩展支持了用户计算机上的本地文件，[官方文档传送门](https://developer.mozilla.org/zh-CN/docs/Web/API/Blob);



#### 2.charCodeAt()


#### 3.Blob对象



#### 引入

伴随着nodejs流行，往日被无数后端程序员所不屑诟病的脚本语言Javascript的重要性与日俱增，2017年IBM一项调查数据显示，目前为止这个小巧灵活的语言已经跃升至用户量第一的编程语言；

Express作为nodejs官方首推的Web框架，也发挥出了巨大的潜力，Express团队现在正在开发更加小巧灵活的下一代nodejs框架KOA，相信也会让很多开发者眼前一亮。
为什么中间件这么重要，试想以下场景，如何解决：
 1.开发过程中在处理http请求过程中，我们需要对请求对象、响应对象做某些特殊预处理工作，最后才会将处理的结果作为响应发送给请求；
 2.请求处理http请求时，需要对所有的请求进行预先处理，比如检查请求的头信息是否存在必须的字段，检验请求的合法性，并做响应拦截过滤；

基本上有两种方案可以解决以上问题：

- 在每处请求响应出都定义中间处理函数，最终做出响应；
- 定义全局的中间处理函数，在各处请求响应中进行引用；

是的，express中间件要解决的问题正是我们以上的需求。


#### 简介

> Express是一个路由中间件Web框架，其自身只具有最低程度的功能，即:一系列中间件函数的调用。

## express **中间件**函数的特点及作用

1. 特点：中间件函数能够访问请求对象(req)、响应对象(res)、下一个中间件函数(next)
2. 作用：①对请求对象进行处理；②对响应对象进行处理；③执行任意自定义功能；④调用下一个中间件；⑤结束请求响应循环；

先来看一个最最简单的Hello world  Express应用程序示例：

```
var express=require('express');
var app=express();
app.get('/',function(req,res){
  res.send('Hello world!')
  })
app.listen(3000);
```  

现在我们用一个最简单的中间件来实现：在GET 方法请求根路径`/`时，先在服务窗口打印出'Response with middleware is working ok.'，再响应输出’Hello World!’

```
var express=require('express');
var app=express();
app.get('/',function(req,res,next){
  console.log('Response with middleware is working ok.');
  next();
  },function(req,res){
  res.send('Hello world!')
  })
app.listen(3000);
```  
