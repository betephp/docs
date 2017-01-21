# 数据库

BetePHP可以使用Raw SQL，Query Builder和ORM方式操作数据库，目前只支持MySQL数据库。

## 配置
数据库配置文件位于`config/database.php`下，你可以定义多个数据库连接，并指定默认的数据库连接。

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

### 读写分离配置
有些时候，你的数据库架构可能是一主一从，或者多主多从，这时候，你可以读写分离配置来配置你的数据库连接。


## 事务
DB::transaction(function () {
    DB::table('users')->update(['votes' => 1]);

    DB::table('posts')->delete();
});
