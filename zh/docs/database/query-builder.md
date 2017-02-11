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
获取结果时默认时获取所有列的数据，你可以使用`select()`指定你需要获取的列。

```php
$users = DB::table('user')->select('id', 'username')->all();
```

`distinct()`可以结果集只包含不重复的数据：

```php
$users = DB::table('user')->select('birthday')->distinct()->all();
```

### Where

`where()`大部分情况使用三个参数，第一个是字段名，第二个是操作符，第三个是做条件比较的值。

```php
$users = DB::table('user')->where('id', '<', 100)->all();
```

为了方便起见，当使用两个参数调用`where()`时，参数第二个则是做比较的值，操作符则默认为`等于`比较。

```php
$user = DB::table('user')->where('id', 123)->first();
```

`where()`支持以下条件比较方式

```php
DB::table('user')->where('id', '>', 1)->first();
DB::table('user')->where('name', 'Ecco')->first();
DB::table('user')->whereRaw('name IS NULL')->first();

DB::table('user')->where('name', 'like', '%name%')->all();
DB::table('user')->where('name', 'not like', '%name%')->all();

DB::table('user')->where('name', 'between', [10, 100])->all();
DB::table('user')->where('name', 'not between', [10, 100])-> all();

DB::table('user')->where('name', 'in', [1, 2, 3])-> all();
DB::table('user')->where('name', 'not in', ['name', 'ecco', 'world'])-> all();

DB::table('user')->where('name', '!=', null)->first();
DB::table('user')->where('name', '=', null)->first();
```


### Order By

```php
$users = DB::table('user')->orderBy('name', 'desc')->all();
```

### Group By

```php
$users = DB::table('user')
    ->groupBy('account_id')
    ->having('account_id', '>', 100)
    ->all();
```

### Limit & Offset

```php
$users = DB::table('user')->offset(10)->limit(5)->all();
```

### Insert

```php
DB::table('user')->insert(
    ['name' => 'Jack', 'email' => 'jack@example.com']
);
DB::table('user')->insert([
    ['name' => 'Jack', 'email' => 'jack@example.com'],
    ['name' => 'Micheal', 'email' => 'micheal@example.com'],
]);
```

### Update

```php
DB::table('users')->where('id', 1)->update(['email' => 'hello@example.com']);
```

### Increment & Decrement

```
DB::table('user')->increment('score');
DB::table('user')->decrement('score');

DB::table('user')->increment('score', 5);
DB::table('user')->decrement('score', 5);
```

### Delete

```php
DB::table('user')->where('id', '=', 1)->delete();
DB::table('user')->delete(); // it will delete all the row in user table.
```

### Lock

```php
DB::table('user')->where('votes', '>', 100)->lockForUpdate()->all();
```
