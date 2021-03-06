> 先做个广告 [Javascript生态](http://stateofjs.com/) 

## 1. 设计模式相关
> 1. 响应式/函数式编程：Rxjs-Reactive extention for javascript
> 2. 面向对象式编程：   OOP -Object Oriented Programming
> 3. 迭代器模式编程：   Iterator Pattern（ES6中可迭代对象：Array、String、Map、Set、DOM data structures）

## 2. Back-end

|序号| 范围 |名称     |作用     |使用场景|相关信息|
|---|---  |---      |---     |---|----|
| 1 |数据库|mySQL    |后台数据库|暂无|[官网](https://www.mysql.com/cn/)|
| 2 |数据库|php      |数据库脚本||[官网](http://php.net/)|
| 3 |数据库|Nodejs   |数据库脚本|事件驱动、非阻塞I/O模型|[官网](https://nodejs.org/zh-cn/)|

  2.1 后端框架

  |序号   |  名 称  |所属语言  |模板引擎 |相关技术|
  |------|---------|--------|--------|-----------|
  |1     |Laravel  |php     |blade   ||
  |2     |SpringMVC|JAVA    |thymeleaf|
  |3     |Express  |Nodejs  |jade、ejs、handlerbar|热部署工具[PM2](http://pm2.keymetrics.io/)、[Forever](http://blog.fens.me/nodejs-server-forever/)、strongloopPM|
  |4     |KOA      |Nodejs  |||

> [KOA 、Express、Hapi三大框架对比](http://www.cnblogs.com/souvenir/p/6039990.html)


## 3. 前端构建工具

|序号|类别              |名称    |作用(范围)              |star|特点|官网|
|---|-----------------|-------|-------------------|-------:|---|----|
|1  | JS包管理器       |npm     | JavaScript包管理器 |13,284+| |[官网](https://www.npmjs.com/)|
|2  | JS包管理器       |yarn    | JavaScript包管理器 |26,461+| |[官网](https://yarnpkg.com/lang/en/)|
|3  | 前端项目打包压缩  |webpack  | 所有资源          |30,423+| |[官网](https://webpack.js.org/)|
|4  | 前端项目打包压缩  |gulp     | js、css、html    |26,924+| |[官网](https://gulpjs.com/)|
|5  | 前端项目打包压缩  |grunt    | js、css、html    |11,508+| |[官网](https://gruntjs.com/)|
|6  | 前端项目打包压缩  |bower    | js、css、html    |15,171+| |[官网](https://bower.io/)|
|7  | 前端项目打包压缩  |browserify| js、css、html   |11,201+| |[官网](http://browserify.org/)|


## 4. Front-end
### 4.1 前端框架

> 不同框架性能对比测试，[传送门](https://rawgit.com/krausest/js-framework-benchmark/master/webdriver-ts/table.html)

|序号|名称     |团队      |设计模式      |star   |包大小(gzip)      |学习曲线|相关技术|相关信息    |
|---|---------|---------|------------|------:|----------------:|-------|-------|--------|
|1  |angularjs|谷歌      |双向数据绑定  |56,105+|                 |陡峭   |MVC|[官网](https://angularjs.org/) |
|2  |angular  |谷歌      |双向数据绑定  |26,225+|237.41kb/v4.1.3|陡峭|MVC、组件化、Rxjs|[官网](https://angular.io/)  |
|3  |react    |facebook |单向数据绑定   |71,926+|46.45kb/v15.5.4|适中|MVC、组件化、React+Flux+JSX状态存储|[官网](https://facebook.github.io/react/)|
|4  |vue.js   |尤雨溪（国内个人)|双向数据绑定|61,363+|28.90kb/v2.3.4  |简单|MVC、组件化、    |[官网](https://cn.vuejs.org/)|
|5  |Polymer  |谷歌赞助        ||17,815+|129.89kb/v2.13.3| |组件化，类似vue  |[官网](https://www.polymer-project.org/)|
|6  |ember    |               ||17,956+|129.89kb/v2.13.3|陡峭|全能框架、大量约定 |[官网](https://www.emberjs.com/)|
|7  |Riot.js  |               ||12,042+||   |轻量级        |[官网](http://riotjs.com/)|
|8  |knockout.js|*可学习,不推荐使用*|| 8,249+||适中|MVVM     |[官网](http://knockoutjs.com/),兼容IE9,

### 4.2 模板引擎技术

- ejs       Javascript模板--[官网](http://ejs.co/)
- jade      js+html模板-----[官网](http://jade-lang.com/)
- blade     php 模板--------[官网](https://laravel.com/docs/5.4/blade)
- Smarty    php 模板--------[官网](https://github.com/smarty-php/smarty)
- thymeleaf JAVA模板--------[官网](http://www.thymeleaf.org/)

各路模板比拼：
![](/sources/imgs/template.png)



### 4.2 css及icon类库

> css样式兼容性测试，[传送门](http://caniuse.com/)

|序号|名称|类别 |说明| 相关信息|
|----|---|---|---|---|
|1   |sass|      |样式文件、CSS预处理器|[官网](http://sass.bootcss.com/)、[入门1](http://www.ruanyifeng.com/blog/2012/06/sass.html)、[入门2](https://www.oschina.net/question/12_44255)|
|2   |fontawesome|图标、样式库 |50,716+            |[官网](http://fontawesome.io/)、[中文官网](http://fontawesome.dashgame.com/)|
|3   |iconfont   |图标、样式库 |阿里出品            |[官网](http://www.iconfont.cn/)|
|4   |gliphyicon |图标、样式库 |Author:Jan Kovarik |[官网](http://glyphicons.com/)|

### 4.3 动画类库

|序号|名称         |技术类型            |Star指数|备注|说明|
|---|-------------|------------------:|-----|------|-----|
|1  |animate.css  |CSS (55.2kB)      |42,557+|63种纯CSS过度动画效果|[案例](https://daneden.github.io/animate.css/)|
|2  |hover.css    |CSS               |16,828+|丰富的悬停效果amazing|[案例](http://ianlunn.github.io/Hover/)|
|3  |magic.css    |CSS (36.5kB)      |4,915+ |丰富的渐变效果       |[案例](https://minimamente.com/example/magic_animations/)|
|4  |Dyncss.css   |CSS               |386+   |页面滚动动画         |[案例](http://www.vittoriozaccaria.net/dyncss-example/)|
|5  |favico.js    |JavaScript        |7,538+ |添加各种徽章效果      |[github](https://github.com/ejci/favico.js/tree/v0.4.0)
|6  |Textillate.js|JavaScript        |2,985+ |添加各种文字动画效果   |[案列](http://textillate.js.org/),依赖:[animate.css](https://daneden.github.io/animate.css/)、[lettering.js](http://letteringjs.com/)|
|7  |bounce.js    |JavaScript        |5,056+ |提供强大的弹性css动画|[案例](http://bouncejs.com/)|
|8  |Move.js      |JavaScript        |4,042+ |css动画            |[案例](http://visionmedia.github.io/move.js/)|
|9  |AniJS.js     |JavaScript        |3,087+  |事件动画效果         |[案例](http://anijs.github.io/)|
|...|pace.js      |JavaScript        |12,053+|网页交互进度提示：ajax/http进度条 |[案例](http://github.hubspot.com/pace/docs/welcome/)|


## 4 可视化工具

|序号  |名称          |团队       |技术基础|star指数|备注   |说明|
|-----|--------------|----------|--------------|-------:|------|-----|
|1    |D3.js         |          |              |        |      |     |
|2    |hightcharts   |歪果仁     |Javascript    |        |[官网](https://www.highcharts.com/)     |     |
|3    |Chart.js      |google    |js+canvas     |+30,737|[官网](http://www.chartjs.org/)      |     |
|4    |Echarts2      |百度       |js            |+18,719|[官网](http://echarts.baidu.com/echarts2/)  |     |
|5    |G2            |阿里—蚂蚁金服|js           |+592    |[官网](https://antv.alipay.com/)、[gihub](https://github.com/antvis)|G6/G2-mobile||

[简单粗暴的动车通道](https://www.zhihu.com/question/19929609)


## 5. Program tools
 1.  Jquery     ——前端入门级别插件库，主要用于调用DOM操作 [英文官方网站链接](https://jquery.com/)，[中文推荐非官方链接](http://hemin.cn/jq/)
 2. Underscore ——函数式编程的功能集，提供一系列远超过map、filter、invoke等方法，涵盖函数绑定、js模板、创建索引，强类型测试等，[英文官方网站链接](http://underscorejs.org/) ，[中文官方链接](http://www.bootcss.com/p/underscore/)
 3. moment.js  ——JS时间处理插件，肥肠强大，[英文官方网站链接](https://momentjs.com/)， [中文官方链接](http://momentjs.cn/)
 4. rxjs       ——观察者模式，强大的函数式编程插件  [入门介绍传送](https://segmentfault.com/a/1190000008809168#articleHeader11)，[英文官方网站链接](http://reactivex.io/rxjs/)，[推荐非官方中文文档](https://buctwbzs.gitbooks.io/rxjs/content/operators.html)
 5. mock.js    ——一个模拟数据生成器，可以让前端独立于后端进行开发。主要功能：生成随机数据，拦截Ajax,适用场景：后端api未开发法完成，但数据格式已经确定。[官网](http://mockjs.com/)、[Github](https://github.com/nuysoft/Mock)
 6. alasql.js  ——客户端数据库操作插件，用户web浏览器js内存中的数据库操作插件，可配合nodejs使用；[官网](http://alasql.org/)、[github](https://github.com/agershun/alasql) star:+1910
 7. lokijs     ——客户端操作数据库插件，alasql.js替代插件，[官网](http://lokijs.org/#/)、[github](https://github.com/techfort/LokiJS) star +3，428:

## 6. SPA项目的SEO解决方案

> 目前spa页面的最大缺点莫过于搜索引擎的友好型很差，所以需要慎重考虑使用场景；
- SEO.js ：针对google搜索引擎,使单页面应用可被爬虫爬取的插件，[官网](http://getseojs.com/)
- Fate :百度针对SPA的工具库 [官网](http://fate.baidu.com/)
![](/sources/imgs/baiduFate.png)
