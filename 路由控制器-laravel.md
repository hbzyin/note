# Laravel 的HTTP控制器
> laravel允许在路由文件中以闭包的形式定义定义所有的请求处理逻辑；同时也支持使用控制器类来阻止路由相关的操作。laravel的控制器将相关的请求处理逻辑组织成一个单独的类，路由控制器类放在`app/Http/Controllers`目录下。
- Laravel 控制器均继承自Laravel内置的基础控制器类；
- Laravel 内置的基础控制器类提供一些便捷的方法，如`middleware`方法可以用来给控制器添加中间件；


### 1. 基础控制器类
控制器命名注意点：
  1. 控制器类定义是必须指定命名空间:`namespace App\Http\Controllers\UserController;`
  2. 注册路由控制器：
    1. 注册路由+控制器指定方法 `Route::get('user','UserController@index');`
    2. 注册路由+单一操作控制器：`Route::get('userinfo/{id}','UserInfoController');`（单一操作控制器无需指明方法）
  4. 控制器路由中使用中间件：
    1. 路由文件中指定中间件：`Route::get('user','UserController@store')->middleware(auth);`
    2. 控制器构造方法指定中间件：
    ```
    namespace App\Http\Controllers;
    class UserController extends Controller{
      public function __constructor(){
        $this->middleware('auth');                        // 默认所有所有路由使用中间件
        $this->middleware(‘log’)->only('index');          // 指定路由使用中间件
        $this->middleware('subscribed')->except('store'); // 指定路由不是使用中间件
      }
    }
    ```

### 2. laravel资源控制器
> Laravel资源控制器将典型的*CURD*路由指定到一个控制器上，可使用Artisan命令快速创建`php artisan make:controller NameController --resource`，该命令在`app\Http\Controllers\NameController.php`中生成一个控制器，改控制器包含了默认的7中可利用资源操作方法
1. 注册资源路由：`Route::resource('names','NameController')`
2. 该路由声明会创建多个路由来处理以下7种不同的资源操作  ：
  |序号|动作     |URI               |操作   |路由名称       |备注|
  |---|---------|-----------------|-------|-------------|-------|
  |1  |GET      |`names`          |index  |names.index  |显示names信息/列表|
  |2  |GET      |`names/create`   |create |names.create |创建name视图/表单|
  |3  |POST     |`names`          |store  |names.store  |保存创建的name记录|
  |4  |GET      |`names/{id}`     |show   |names.show   |获取一条name记录|
  |5  |GET      |`names/{id}/edit`|edit   |names.edit   |编辑一条name记录|
  |6  |PUT/PATCH|`names/{id}`     |update |names.update |更新一条name记录|
  |7  |GET      |`names/{id}`     |destroy|names.destroy|删除一条name记录|
