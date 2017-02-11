# Query Builder

BetePHP's Query Builder providers a fluent interface to running database queries, and also use PDO parameter binding to protect your database operation against SQL injection attacks.

### Get all the row/first row from table

```php
use Bete\Database\DB;

# All the rows
$users = DB::table('user')->all();

foreach ($users as $user) {
    echo $user->name;
}

# First row
$user = DB::table('user')->where('id', 1)->first();
echo $user->name;
```

### Get the single column of (all the row)/(first row)

```php
# Get the single column of all the row
$names = DB::table('user')->column('name');
foreach ($names as $name) {
    echo $name;
}

# Get the single column of first row
$name = DB::table('user')->where('id', 1)->value('name');
echo $name;
```

### Chunking results
```php
DB::table('user')->chunk(100, function ($users) {
    // process 100 rows of users.

    return true; //return false if you want stop.
})
```

### Aggregate
```php
$count = DB::table('user')->count();

$birthday = DB::table('user')->max('birthday');
```

### Select
In default, the row you get include all the columns, you can you `select` specify a custom columns.

```php
$users = DB::table('user')->select('id', 'username')->all();
```

`distinct()` let result collection only include the no-repeated data.

```php
$users = DB::table('user')->select('birthday')->distinct()->all();
```

### Where

You pass three arguments to `where()` when using it: the first is the column name, the second is an oprator, the third is the value to compare.

```php
$users = DB::table('user')->where('id', '<', 100)->all();
```

If you simply want to verify that a column is equal to a given value, you may pass the value directly as the second argument to the `where()` method:

```php
$user = DB::table('user')->where('id', 123)->first();
```

`where()` support the below condition:

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
