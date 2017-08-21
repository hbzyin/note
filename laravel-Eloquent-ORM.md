# Laravel ORM---对象关系映射

> ORM：Eloquent Relationship Mapping 一种程序技术，用于实现面向对象编程语言里面不同类型系统的数据之间的转换；其效果是：创建了一个在编程语言里可用的“虚拟对象数据库”；

## 1. 创建model
- 数据表模型 `php artisan make:model ModelName -m`

```
<?php
namespace App;

use Illuminate\Database\Eloquent\Model;
class ModelName extends Model{
    // 1. 定义数据模型关联的表
    protected $table = 'ModelNames';

    // 2. 重定义主键 ,eloquent默认主键‘id’
    $primaryKey='id';

    // 3. 时间戳 eloquent默认你的数据表里面有'created_at'、'updated_at'字段，
    //    如果不想让eloquent西东维护这连个字段，可将$timestamps属性设置为false
    //    如果要自定义时间戳格式，可设置 $dateFormat属性；
    public $timestamps=false;
    protected $dataFormat='U';

    //  4. 数据库链接 eloquent模型会使用应用程序中默认数据库链接，自定义设置$connection
    protected $connection='connection-name';

//$fillable、$guarded两个字段不可同时存在，通常只设置一个参数
    // 5.1 设置可修改字段，其他字段不可修改
    protected $fillable=['name','telephone'];

    // 5.2 设置保护（不可修改字段）其他字段均可修改
    protected $guarded=['id','created_at'];

}
```
- 数据 Repository实例

```
<?php

use App\ModelName;
// 5. eloquent模型可以作为强大的查询构造器，流畅的查询与模型关联的数据表
// 5.1 查询所有
$modelnames=App\ModelName::all();
foreach($modelnames as $modalname){
  echo $modalname->name;
}
// 5.2 条件查询 ：先添加查询条件，最后用get()获取查询结果
$modalnames1=App\ModelName::where('id' 1)
              ->orderBy("name",'desc')
              ->take(10)
              ->get();
>
```

## 2. 操作模型


#### 2. 1 查询

- 集合： `get`、`all`方法可以取回多个结果；返回值为`Illuminate\Database\Eloquent\Collection`实例；`Collection`类提供**多种辅助函数**用来处理Eloquent结果；如：`foreach()`
- 分块结果：取回大量数据的部分进行处理，优化内存 `chunk`,如：`ModelName::chunk(200,function($modelnames){foreach($ModelNames as $Modelname)})`
- 使用游标：`cursor`
- 取回单个模型/集合： `find(1)`、`first()`、`find([1,2,3])`、`findOrFail(1)`、`firstOrFail()`;
- 取回集合：`count()`-数量、`sum()`-、`max()`-最大值

#### 2. 2 更新模型

- 更新数据 `save()`,如：
```
$flight = App\Flight::find(1);        // 1. 取回记录
$flight->name = 'New Flight Name';    // 2. 修改记录属性
$flight->save();                      // 3. 保存修改
```
- 批量更新 `update()`如：

```
// 将所有actve=1;destinamtion='Being'的数据标识为延迟
App\Flight::where('active',1)
            ->where('destination','Beijing')
            ->update(['delayed'=>1])

```

#### 2.3 创建数据


- 添加数据：`save()`,如下例：

```
<?php
namespace App\Http\Controllers;
use App\Flight;
use Illuminate\Http\Request;
use App\Http\Controllers\Controller;
class FlightController extends Controller{
    /**
     * 创建一个新的航班实例。
     * @param  Request  $request
     * @return Response
     */
    public function store(Request $request)
    {
        // 验证请求...
        $flight = new Flight;           // 1. 新建实例
        $flight->name = $request->name; // 2. 设置属性值
        $flight->save();                // 3.保存实例
    }
}
```
- 批量添加：`create()` 如：
```
// 1 没有实例新建
$flight=App\Flight::create(['name'=>'flight10'],['name'=>'flight11'])
// 2 已有实例新建
$flight->fill(["name"=>"flight12"]);
```
- 其他创建方法：`firstOrCreate()`-尝试查找，找不到时，使用指定属性添加新记录到数据库、`firstOrNew()`-尝试查找，找不到时，返回一个模型实例，需手动调用save()保存到数据库

#### 2.4 删除模型
- 取回实例，删除实例：`delete()`,如：
```
$flight=App\Flight::find(1);    // 1. 查找到需删除实例
$flight->delete();              // 2. 删除实例
```

- 通过键直接删除
```
App\Flight::destroy(1);
App\Flight::destroy(1,2,3);
App\Flight::destroy([1,2,3]);
```
- 条件删除：通过查询语句来删除：
```
$deleteRows=App\Flight::where('active',0)->delete();
```

#### 2.5  软删除 --删除Eloquent模型

> 软删除模型，即Eloquent仅删除ORM模型，真实数据并不会从数据库中删除；同时会在模型上设置一个`deleted_at`属性，如果一个模型`deleted_at`属性值非空，则代表模型已经被软删除了；
> 要启动模型上软删除功能，需要在模型上使用`Illuminate\Database\Eloquent\SoftDeletes`trait并添加`deleted_at`字段到`$dates`属性上；
> 启用软删除时，被软删除的的模型会自动从所有查询结果中排出；

- 启用软删除
```
<?php
namespace App;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;
class Flight extends Model{
    use SoftDeletes;
    /**
     * 需要被转换成日期的属性。
     * @var array
     */
    protected $dates = ['deleted_at'];
}
```

- 启用软删除后，查询结果包含软删除模型：`withTrashed()`,如：

```
$flights=App\Flight::withTrashed()
                ->where('account_id',1)
                ->get();

```
- 启用软删除后，只查询出软删除数据：`OnlyTrashed()`
```
$flight=App\Flight::OnlyTrashed()
        ->where('airline_id',1)
        ->get();
```
- 恢复软删除的模型:`restore()`
```
$flight->restore();//回复单个软删除模型
App\Flight::withTrashed()
          ->where('airline_id','>',1)
          ->restore();
```
- 永久删除模型：`forceDelete()`
```
// 1. 强制删除单个模型
$flight->forceDelete();
// 2. 强制删除所有相关模型
$flight->history()->forceDelete();
```



## 3. 事件

Eloquent模型会触发很多事件，给用户在模型的生命周期多个时间点进行监控：
`creating`、`crated`、`updating`、`updated`、`saving`、`saved`、`deleting`、`deleted`、`restoring`、`restored`;
这些事件在调用前需要在Eloquent模型上定义一个`$events`属性，并将声明周期映射到服务提供者；
```
<?php

namespace App;

use App\Events\UserSaved;
use App\Events\UserDeleted;
use Illuminate\Notifications\Notifiable;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable
{
    use Notifiable;

    /**
     * 模型的时间映射。
     *
     * @var array
     */
    protected $events = [
        'saved' => UserSaved::class,
        'deleted' => UserDeleted::class,
    ];
}
```

## 4. 观察者：
> 用户可自定义模型监听事件的集合类，来反应Eloquent监听的时间，每个方法接受model作为其唯一参数;使用观察者，需要两个步骤：
- 定义观察类：

```
<?php
namespace App\Observers;
use App\User;
class UserObserver{
    // 监听用户创建的事件。
    public function created(User $user) {
        // do something here...
    }

    // 监听用户删除事件。 *
    public function deleting(User $user){
        // do other thing here ...
    }
}
```

- 注册观察者类：

```
<?php
namespace App\Providers;

use App\User;
use App\Observers\UserObserver;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider{

    //  注册观察者类 --运行所有应用  
    public function boot(){
        User::observe(UserObserver::class);
    }

    // 注册服务提供.
    public function register() {
        //
    }
}
```
