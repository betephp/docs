# Database

BetePHP support three ways to operate with Database: Raw SQL, Query Builder and ORM. The database driver only support MySQL right now.

## Configure
Database configuire file is at `config/database.php`, you can configure multiple database connnections, and designate a default one.

```
<?php

return [

    'fetch' => PDO::FETCH_OBJ,

    'default' => 'default',

    'connections' => [

        'default' => [
            'driver' => 'mysql',
            'host' => ini('DB_HOST', 'localhost'),
            'port' => ini('DB_PORT', '3306'),
            'database' => ini('DB_DATABASE', 'test'),
            'username' => ini('DB_USERNAME', 'root'),
            'password' => ini('DB_PASSWORD', 'root123'),
            'charset' => 'utf8',
            'prefix' => '',

            // 'write' => [
            //     ['host' => '', 'port' => ''],
            //     ['host' => '', 'port' => ''],
            // ],

            // 'read' => [
            //     ['host' => '', 'port' => ''],
            //     ['host' => '', 'port' => ''],
            // ],
        ],

    ],

];
```

### Read & Write
Sometime, your database architecture maybe have one master, one slave, or multiple masters or multiple slaves, you can use read/write to configure it.


## Transaction

```php
DB::transaction(function () {
    DB::table('users')->update(['votes' => 1]);

    DB::table('posts')->delete();
});
```
