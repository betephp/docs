# Query Builder

BetePHP的Query Builder让你可以通过非常流畅的链式表达方式操作数据库，同时链式操作使用PDO参数绑定特性防止SQL注入。

### 从数据表取出所有行/第一行

```php
use Bete\Database\DB;

# 所有行
$users = DB::table('user')->all();

foreach ($users as $user) {
    echo $user->name;
}

# 第一行
$user = DB::table('user')->where('id', 1)->first();
echo $user->name;
```
`all()`方法返回一个包含所有结果集的`Bete\Support\Collection`对象，每个结果是一个StdClass对象，你可以StdClass的属性访问每个结果的列值。

### 获取所有行的单列/第一行的单列值

```php
# 获取所有行的单列
$names = DB::table('user')->column('name');
foreach ($names as $name) {
    echo $name;
}

# 第一行的单列值
$name = DB::table('user')->where('id', 1)->value('name');
echo $name;
```

### 分批获取结果
```php
DB::table('user')->chunk(100, function ($users) {
    // process 100 rows of users.

    return true; //return false if you want stop.
})
```

### 聚合
```php
$count = DB::table('user')->count();

$birthday = DB::table('user')->max('birthday');
```

### Select

### Where

### Order, Group By, Limit, Offset

### Insert

### Update

### Increment & Decrement

### Delete

### Lock

