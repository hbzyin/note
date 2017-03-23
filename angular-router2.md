## Angular2 导航方式
### 预警
> 1.导航方式

> 2.参数路由

#### 1. 导航方式

ngular2主要有两种导航方式：

①链接式导航：页面设置导航链接，点击后跳转至相应页面；如：

```html
<a routerLink=['/home']>click here to go to home page</a>
```

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

加入我们现在有一个订单列表页面，需要查看每个订单的详情，改如何导航哪？
a.我们可以为每个订单设置一个连接；b.设置路由跳转规则，导航是带上区别订单的关键字段；
是的，没错，angular2就是采用方式2进行导航的；

 在开始进行参数导航之前，让我们先来了看几个angular2的路由服务的相关术语：
 
 | 序号 | 类别 | 部件          | 名称  | 作用 |
 | --- | ----|:---           | -----   |---- |
 | 1   | |Route              |路由         | 定义路由器如何根据URL模式来导航到组件，大多数都由路径和组件类构成   |
 | 2   |组件 |Router          |路由器       | 为激活的url显示对应的组件，负责从一个页面/组件，导航到另一个页面/组件 |
 | 3   |常量 |Routes          |路由数组     | 定义一个路由数组，每一个都会把一个URL路径映射到一个组件 |
 | 4   |模块 |RouterModule    |路由器模块   | 用于提供所需的服务提供商，提供进行导航的指令|
 | 5   |指令 |RouterLink      |路由链接     | `[routerLink]=['str']`用于把可点击的html元素绑定到路由 |
 | 6   |指令 |RouterOutlet    |路由插座     | `<router-outlet>`用来标记路由该在哪里显示视图|
 | 7   |指令 |RouterLinkActive|活动的路由链接| 当html元素上的routerLink变为激活或非激活状态时，该指令为相应元素添加或移除css类|
 | 8   |方法 |RouterState     |路由器状态   | 路由器的当前状态包含了一颗由程序中激活的路由构成的树，，提供一些用于遍历路有数的快捷方法|
 | 9   |服务 |Activedroute    |激活的路由   | 为每个路由组件提供一个服务，包含特定的路由信息，如：路由参数、静态数据、解析数据、全局查询参数、群居碎片 |
