## Angular2 路由导航简介

### 剧情透露
>1.浏览器默认路由

>2.Angular2 路由及导航

#### 1、浏览器路由模式

  浏览器默认的导航模式主要有三种：
  
  - ①点击页面链接，跳转至相应页面；
  - ②输入url,点击确认，跳转至相应页面；
  - ③点击浏览器前进后退箭头，进行页面的跳转；

关于浏览器url跳转原理，参靠这两篇：
[1.在浏览器地址栏输入一个URL后回车，背后会进行哪些技术步骤？](https://www.zhihu.com/question/34873227)
[2.输入网址之后发生的事。](https://www.zybuluo.com/yangfch3/note/113028)


#### 2、Angular2 的路由导航

以下内容默认读者对Angular2项目已有初步探索，熟悉angular2的项目目录结构：

##### 1.概述
Angular2默认采用支持html5浏览器的history.pushState进行导航，同时也支持老式的hash(#)风格导航； 
使用Angular2的路由功能简单来说分以下几个步骤：
1. 导入路由模块 
Angular2的路由是一个可选的服务，并不包含在Angular核心库，在单独的@angular/router包中，需手动在src/app/app.module文件中导入，
即： `import{RouterModule,Routes} from '@angular/router;`
2. 设置跟路由
Angular路由默认采用相对文件路径，为了保证项目的正常导航，需要在根目录文件index.html中设置根路径；
即：`<base href="/">`
3. 路由文件配置
至此，就可以尽情的享用angular的路由服务了？然而并未如此，你还要定义你的导航规则，也就要看到真正的导航效果，
你还需要两步要走：
 - ①设置路由配置：在src/app/app.module.ts文件中配置路由参数
 ```typescript
 // 1.angular2 路由采用有限匹配原则，所以通用匹配一般放置在最后；
 // 2.angular2 路由配置文件中路径不能以斜杠slash('/')开头,导航时会自动识别转换；
 // 3.angular2 路由
const appRoutes:Routes=[
    {path:'login',component:LoginComponent},                           //普通路由配置
    {path:'home',component:HomeComponent,data: { title: 'home page' }},//带页面说明信息路由配置
    {path:'pages/:id',component:PagesComponent},                       //带参数路由配置
    {path:'',redirectTo:'/home',pathMatch:'full'},                     //默认路由配置（路由重定向）
    {path:'**',component:PageNotFoundComponent}                        //无效路由配置（通配符）
];
@NgModule({
    imports:[
    RouterModule.forRoot(appRoutes) //此处根模块使用 RouterModule.forRoot()
    //other imports here            //若是子模块使用 RouterModule.forChild()
    ],
    ...
})
export class AppModule{}
```
- ②路由链接设置：至此我们只要在html页面中设置路由链接、组件视图渲染位置遍可以自由导航了；

```angular2html
// 1. 路由链接：导航地址         routerLink='string'
//            当前导航是否可用   routerLinkActive='active'
// 2. 路由插座：组件视图渲染位置  <router-outlet></router-outlet>
template:'
    <h1>Angualr2 Router</h1>
    <nav>
        <a routerLink="/home" routerLinkActive="active">Home page</a>
        <a routerLink="/pages/:id" routerLinkactive="active">Detail page</a>
    </nav>
    <router-outlet></router-outlet>
'
```
- PS:angular在导航是每个生命周期成功完成时，路由器会构建一个ActivedRoute组成的树，表示路由器的当前状态。
我们可以在应用中的任何地方使用Router服务，以及routerState属性来访问当前RouterState值。


```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/hbzyin/blog/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
