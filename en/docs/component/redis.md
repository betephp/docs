# Redis

## Configure
Redis configure file is `config/redis.php`, you can configure multiple redis connection, and designate a default one.

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

## Usage

```php
// Using the default connnection.
app()->redis->set('key', 'value');
app()->redis->get('key');

// Using the second connection.
app()->redis->connection('second')->set('key', 'value');
app()->redis->connection('second')->get('key');
```
Redis detail documentation see: [https://github.com/phpredis/phpredis](https://github.com/phpredis/phpredis)
