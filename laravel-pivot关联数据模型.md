## 数据透视表和多对多关联

 注：本篇文章纯属翻译
原文链接：[http://laraveldaily.com/pivot-tables-and-many-to-many-relationships/](http://laraveldaily.com/pivot-tables-and-many-to-many-relationships/)

> 今天主要探讨一下Laravel框架中，一个可能不怎么容易理解但是却非常实用的一个概念:数据透视表(原文`pivot table`，个人认为称为关联表更合适，下文所提及关联表，即此处的数据透视表)。数据透视表是一种两张主表相互关联组成的关联表的一种。

#####  1. 实际场景中的例子：数据透视表

laravel官方文档中给出了一种**用户-角色(`User-Role`)**关系的例子。在这个例子中，一个用户可能于多个角色对应，反过来同理，一个角色也可能对应多个用户。这里为了清楚说明这个概念，这里选取一个生活中更常见的例子：**商店-商品(`Shops-Products`)**.

我们知道，通常情况下，一个公司在不同的地区会有很多商店，同时也会拥有各种各样的产品。这是一个典型的多对多的关系：
- 一个商品可以从属于多个不同的商店；
- 一个商店会拥有各种不同的产品；

现在已最简单的数据解构为例进行说明：
- 商店数据表**`shops`** ：`id`、`name`
- 商品数据表**`products`** : `id`、`name`
- 商店-商品数据表**`product_shop`** : `products_id`、`shop_id`

在这个场景中，`product_shop`数据表，就是我们所要说明的`pivot`表（及本文的主要说明对象），首先做一下几点说明：
- 关联表名称：关联表的命名满足一下两点：①需包含相关联的单表的表名；②以下划线`_`链接相关联表名；③通常以字母先后顺序来确定相关联表名的先后顺序；如本例中关联表可叫做`product_shop`而不是`shop_product`或者其他名字；
- 创建关联表：创建关联表,一般常见一个简单的命令`artisan make:migration`或`artisan make:migration:pivot`.
- 关联表键名：通常情况下，每个关联表需要有两个外键字段，每个外键对应一张外联表，在我们的商店-商品场景中，这两个外键分别是`product_id`、`shop_id`；当然如果你喜欢你也可以添加更多的字段，但那中情况下，你需要添加更多的关系，这种情况我们稍后会进一步说明；

##### 2. 多对多关系中的模型：`BelongsToMany`

有了数据表和迁移数据，现在我们来创建数据模型；这里的主要工作是定义多对多关系，你可以在任意一个你喜欢的相关关系‘主’表中进行定义，如我们场景中的商店或商品数据模型中；
1. 创建关联表
  1. 方案1-在商店主表中创建多对多关联数据模型：

```
//app/Shop.php
class Shop extends Model{
  public function products(){
    return $this->belongsToMany('App\Products');
  }
}
```

  2. 方案2-在商品数据模型中创建多对多关联数据模型：

```
// app/Product.php
class Products extends Model{
  public function shops(){
    return $this->belongsToMany(’App\Shops');
  }
}
```
2. 自定义命名关联表
实际开发过程中，采用哪种方式取决于你的需求，甚至你可以同时采用两种方式分别定义关联表。完成关联表定义后，Laravel默认创建的关联表遵守一定的命名规律命名关联表：联合命名,如本例默认关联表名为`product_shop` ；如果你需要自定义关联表名称，你需要传入第二个参数，假如你需要将生成的关联表命名为`products_shops`:
```
public function products(){
  return $this->belongsToMany('App\Products','products_shops')
}
```

3. 自定义关联表键名：
同关联表命名类似，Laravel默认会采用单数形式进行来命名关联表的键名，如本例中，默认关联表的键名为`product_id`、`shop_id`,如果你需要自定义命名生成关联表的键名，你需要传入更多的参数，假如你需要将生成的关联表键名命名为`products_id`、`shops_id`,你可以进行如下操作；
```
public function products(){
  return $this->belongsToMany('App\Products','products_shops','shops_id','products_id');
}
```

> 多对多关联表的主要优点在于：**你不需要额外创建关联表*，便可以通过关联数据模型对关联数据进行管理**。下面我们便来介绍如何通过关联模型进行关联数据管理。

##### 3. 多对多关联数据的管理：` attach-detach-sync`

现在我们已经创建好了商店数据表、商品数据表以及各自的模型。现在我们来说明如何通过两个数据模型，而不是通过第三张中间表来进行数据的管理；

1. 场景1：向商店中增加一条商品记录：
```
$shop=Shop::find($shop_id);
$shop->products()->attach($product_id);
```

2. 场景2：向商店中删除一条商品记录：
```
$shop=Shop::find($shop_id);
$shop->products()->detach($product_id);
```
3. 场景3：向商店中删除所有商品记录：
```
$shop=Shop::find($shop_id);
$shop->products()->detach();
```

4. 场景4：向商店中增加多条商品记录：
```
$shop=Shop::find($shop_id);
$shop->products()->attach([123,456,234]);
```
5. 场景5：向商店中删除多条商品记录：
```
$shop=Shop::find($shop_id);
$shop->products()->detach([13,56,34]);
```

6. 复合操作：

在使用过程中，另外一些非常实用的方法，比如更新整个关联表，假如你是一个地区商店的管理员，你需要同时管理多个商店或多种商品，这时候，你需要同时勾选中所有需要操作的数据（商店/商品）,比如所有商店，然后同时删除/添加多种商品；如果一条一条的进行操作，那真是太麻烦了；庆幸的是，Laravel提供了一个`sync()`的方法，这个方法接受一个`Array`类型的参数；
`$product->shops()->sync([1,2,3])`

无论之前关联表里面有多少数据，执行以上操作后，关联表里面将只有三条数据，即`product_shop`关联表里面将只剩下`shop_id`为1,2,3的数据；

##### 4. 自定义关联表额外的属性键

1. 添加额外属性到关联表：`withPivot('key1',key2,...)`
如前所述，在开发过程中，开发人员在关联表中添加额外的属性字段也是比较常见的场景，如我们可能需要在`product_shop`关联表中添加类似于商品数量、价格、更新时间等字段`amount`、`price`、`timestamps`；这是需要做的仅仅是在`migration`文件中增加几个额外的属性字段，如：
```
public function products(){
  return $this->belongsToMany('App\Products')
          ->withPivot('products_amount','price')
          ->withTimestamps();
}
```
2. 展示额外属性字段`->pivot()`
添加额外属性字段后，我们如何获取添加的额外属性字段那？laravel提供了`pivot`方法来调用额外属性字段；
```
foreach($shop->products as $product){
  echo $product->pivot->price;
}
```

3. 保存额外属性字段信息：`attach(main_key,[extra_key1=>value1,extra_key2=>value2])`
当我们修改了添加的额外属性信息时，如何进行保存那，同保存默认属性一样，调用`attach`方法
`$shop->products()->attach(1,['product_amount'=>100,'price'=>49.99])`

###### 总结
> 关联表`pivot tables`和多对多关系数据，可以很方便的运用laravel提供的Eloquent进行处理；而无需额外创建新的关联数据表。
