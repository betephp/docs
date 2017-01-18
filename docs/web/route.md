# 路由

框架默认的路由是将controller/action的请求路由到App\Http\Controller\Action.php文件，如果需要配置多个路由。


## 默认路由器
框架默认的Controller是Home，可以安装如下配置需要的默认Controller。
```
return [
    'default' => 'post',
    'rules' => [
        'doctor/<id:\d+>' => 'doctor/info',
    ],
];
```

## 自定义路由
你可以使用```config/route.php```配置文件自定义配置你的路由规则。
```php
return [
    'rules' => [
        'doctor/<id:\d+>' => 'doctor/info',
    ],
];
```
将docotr/12345的请求路由到doctor/info?id=12345。