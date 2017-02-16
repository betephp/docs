# BetePHP

BetePHP is a lightweight, high performance PHP framework. we believe a good PHP framework should be simple, clean and don't effect performance too much, BetePHP is combined by some frequently used component, without dependency on any composer package, the main feature include:

* Simple, flexible route engine
* High performance
* Fantastic components
* Uniform api style

### Simple, flexible route engine

```php
return [
    'rules' => [
        'order/<id:\d+>' => 'order/info',  # order/1 -> order/info?id=1
        '<sid:\d+>/<gid:\d+>' => 'good/info', # 1234/5678 -> good/info?sid=1234&gid=5678
    ],
];
```

### High performance
Running at single core, 1G memory server, the QPS for each framework is show below: (higher is better)

![Screenshot](/img/performance.png)

### Fantastic components
* Validator
* Log
* Cookie
* Session
* Redis
* ...

### Uniform api style

```php
app()->log->warning('some thing go wrong.');

app()->cookie->set('name', 'value');

app()->session->set('name', 'value');

app()->redis->set('key', 'value');
```
