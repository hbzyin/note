## blade 模板引擎

## 1. 简介
- php模板引擎
- 视图中可使用php代码
- 视图编译成php缓存代码
- laravel存放位置`resources/views`
- 扩展名： `.blade.php`

## 2. 模板继承&区块
- `@section`: 定义视图区块
- `@yield`  : 显示指定区块内容
- `@extends`: 继承页面
- `@include('shared.error')`、`@include('view.name',['some'=>"data"])`
- `@includeIf()`
- `@each('view.name',$jobs,'job')`   : 为集合渲染视图
-  路由`view`返回blade视图：
```
Route::get('blade',function(){return view('child')});
```

## 3. 组件

- `@component('componentName')`：定义组件
- `@component('componentName',['varible'=>'value'])`:定义组件并传参
- `{{$slot}}`: 组件注入位置

> Blade的语法`{{}}`会自动调用php的`htmlspecialchars`函数来避免XSS攻击

  1. `{{isset($name)?$name:'default'}}`   -----php表达式
  2. `{{$name or 'default'}}`             -----blade模板等价于 三元表达式
  3. `{{!! $name !!}}`                   -----不会调用php的`htmllspecialchars`，保留原始值
  4. `@{{}}`                             -----@符号表示Blade渲染影青保留原始状态表达式
  5. `@verbatim`                        ------与4相似，用于显示大片区块中javascript变量

## 4. 控制结构

  1. if表达式： `@if`、`@elseif`、`@else`、`@endif`    
  2. unless表达式：`@unless(Auth::checked())`
  3. 循环    ： `@for($i=0;$i<10;$i++)`、`@foreach($users as $user)`、`@forelse($users as $user);@empty`、`@while(true)`、`@continue`、`@break`、`@break($user->number==5)`
  4. 循环变量 ：`$loop`、`$loop->index`、`$loop->iteration`、`$loop->count`、`$loop->last`、`$loop->depth`、`$loop-parent`、`$loop->first`、`$loop->last`

## 5. 注释
> blade模板返回注释不会渲染到html
`{-- 此注释将不会出现在渲染后的 HTML --}}`

## 6. 嵌入php代码

`@php` ------视图中插入php代码

## 7. 堆栈
  `@push('script')`
 ## 8. 服务注入
 ```
 @inject('metrics','App\Services\MetricsService');  // 注入

 <div>
    Monthly Revenue: {{ $metrics->monthlyRevenue()}}；//
 </div>
 ```
 ## 9. 拓展命令
 - Blade 甚至允许你使用 directive 方法来注册自己的命令。当 Blade 编译器遇到该命令时，它将会带参数调用提供的回调函数
