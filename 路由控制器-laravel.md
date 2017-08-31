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
<<<<<<< HEAD
  3. 控制器路由中使用中间件：
=======
  4. 控制器路由中使用中间件：
>>>>>>> c4f6c7f6da212a597e3e92e83d73ff3a934b9fa2
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
<<<<<<< HEAD
> Laravel资源控制器将典型的*CURD*路由指定到一个控制器上，可使用Artisan命令快速创建`php artisan make:controller NameController --resource`，该命令在`app\Http\Controllers\NameController.php`

##### 1. 默认配置路由资源

=======
> Laravel资源控制器将典型的*CURD*路由指定到一个控制器上，可使用Artisan命令快速创建`php artisan make:controller NameController --resource`，该命令在`app\Http\Controllers\NameController.php`中生成一个控制器，改控制器包含了默认的7中可利用资源操作方法
>>>>>>> c4f6c7f6da212a597e3e92e83d73ff3a934b9fa2
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
<<<<<<< HEAD

##### 2. 自定义路由资源
1. 声明部分路由资源：可指定控制器处理部分操作，而不必使用全部的默认操作如：
```
Route::resource('user','UserController',['only'=>['index','show']]);
Route::resource('user','UserController',['except'=>['store','create']]);
```
2. 重写资源路由:
`Route::resource('user','UserController',['names'=>['create'=>'user.build']])`
3. 重命名资源路由参数：laravel默认基于资源名称的行事生成路由参数；开发者可输入`parameters`参数，实现每个资源基础参数的重写：
`Route::resource('user','UserController',['parameters'=>['user'=>'admin_user']])`;此时，生成show方法路由如下`/user/{admin_user}`
4. 重命名路由方法：开发者可以使用`Route::resourceVerb`方法，在AppServiceProvider的`boot`方法中重写路由方法：
```
use Illuminate\Support\Facades\Route;
public function boot(){
  Route::resourceVerb(['create'=>'add','edit'=>'update']);
}
```
重定义路由方法后`Route::resource('user','UserController')`注册的路由会产生`/user/add`、`/user/{id}/update`的URI;
5. 增加自定义资源路由：若要在默认路由之外增加资源控制路由，需要在`Route::resource`之前定义；否则，`resource`定义的方法会覆盖增加的资源路由：
```
Route::get('user/order','UserOrderController@method');
Route::resource('user','UserController');
```
### 3. 获取路由参数：
> 如要在控制器方法中获取路由参数传递的参数，秩序在其他依赖后列出路由参数即可。如：路由为`Route::put('user/{id}','UserController@update')`的路由获取参数，代码如下
```
<? php
namespace App\Http\Controllers;
use Illuminate\Http\Request;
class UserController extends Controller{
  public function update(Request $request,$id){
  // do job here;
}
}
```

### 4. Laravel路由缓存

> Laravel提供路由缓存，使用路由缓存将极大的减少注册全部应用路由的时间，在Artisan命令中执行`route:cache`即可生成路由缓存
`php artisan route:cache`

- 路由缓存机制仅在基于路由控制器的情况下适用；
- 执行缓存机制后，每次请求都会加载缓存路由文件，增加新的路由是，需要刷新路由缓存；`php artisan route:clear`
-
=======
>>>>>>> c4f6c7f6da212a597e3e92e83d73ff3a934b9fa2
