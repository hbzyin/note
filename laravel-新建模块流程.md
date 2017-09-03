## Laravel框架开发步骤

完成Laravel框架的环境搭建后就是页面的开发了，在有数据库的情况下，需配置好数据库连接，然后进行本篇简述的开发流程：
大概流程如下：
1. 数据模型配置（Model）
2. 抽象层数据仓库配置(Eloquent)
3. 路由配置 （Route）
4. 控制器配置（Controller）
5. 页面配置 （View）

#### 1. DB模型配置
- 创建DB数据库模型：文件路径：`app/Models/`
- 配置功能权限：文件路径`config/admin/global.php`
- 操作权限配置：文件路径`config/admin/permissions.php`

#### 2. Eloquent模型配置
- 创建ORM数据模型：文件路径`app/Repository/`
- 创建Facades映射：文件路径`app/Facades/`
- 配置ORM-controller映射：文件路径`app/Providers/BackendServiceProvider.php`
- 配置ORM-Facades映射：文件路径`config/app.php`

#### 3. 前端Router路由配置
- 配置页面路由：文件路径`app/Http/routes`、`app/Http/Routes/`

#### 4.前端控制器配置
- 配置控制器：文件路径`app/Http/Controllers`


#### 5. 前端view配置
- 创建html文件配置：文件路径`resources/views/`
- 创建外联js文件配置：文件路径`public/backend/js/`
- 创建外联css文件配置：文件路径`public/backend/css/`
- 配置国际化语言：文件路径 `resources/lang/`

#### 6. 页面展示+权限配置
- 菜单管理->添加菜单
- 权限管理->菜单审核
- 权限分配->角色管理权限配置
