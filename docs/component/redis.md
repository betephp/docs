# Redis

## 配置
Redis配置文件见`config/redis.php`，connections中可配置多个Redis连接，default指定默认的Redis连接。

```php
return [

    'default' => 'default',

    'connections' => [

        'default' => [
            'host' => ini('REDIS_HOST', 'localhost'),
            'port' => ini('REDIS_PORT', 6379),
            'password' => false,
            'database' => 0,
            'timeout' => 0,
            'prefix' => 'betephp:',
        ],

        'second' => [
            'host' => ini('REDIS_HOST', 'localhost'),
            'port' => ini('REDIS_PORT', 6379),
            'password' => false,
            'database' => 0,
            'timeout' => 0,
            'prefix' => 'betephp:',
        ],
        
    ],

];
```

## 使用

```php
// 使用默认连接
app()->redis->set('key', 'value');
app()->redis->get('key');

// 使用second连接
app()->redis->connection('second')->set('key', 'value');
app()->redis->connection('second')->get('key');
```
Redis详细文档见 [https://github.com/phpredis/phpredis](https://github.com/phpredis/phpredis)
