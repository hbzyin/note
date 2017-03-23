## Angular2 导航方式
### 预警
> 1.导航方式

> 2.参数路由

#### 1. 导航方式

ngular2主要有两种导航方式：

①链接式导航：页面设置导航链接，点击后跳转至相应页面；如：

`html
<a routerLink=['/home']>
`

②命令式导航：设置点击事件，在组件内进行逻辑页面跳转;如：
```typescript
@Component({
  template:`
  <button (click)="goHome()">主页面<button> //页面跳转事件
  `,
  ...
})
export class AppComponent implements OnInit({
  constructor(){};
  ngInit():void{}
  goDetail():void{                        //跳转处理函数  
    this.router.navigate(['/home']);
  }
})
```

#### 2. 路由传参导航

加入我们现在有一个订单列表页面，需要查看每个订单的详情，改如何导航 哪？
a.我们可以为每个订单设置一个连接；b.设置路由跳转规则，导航是带上区别订单的关键字段；
是的，没错，angular2就是采用方式2进行导航的；

 在开始进行参数导航之前，让我们先来了看几个angular2的路由服务的相关术语：
 
 |    序号     | 部件       | 名称  | 作用 |
 | ---------- | :---      | ------- |---- |
 | 1          | Router    |路由器  |为激活的url显示对应的组件，负责从一个页面导航到另一个页面 |
 | 2          |  32       |       |     |