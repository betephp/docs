# Web路由

默认情况下，框架的首页路由为home/index，如果需要修改，请访问
默认情况下，框架会将`<abc>/<def>`的请求路由到App\Web\<Abc>命名空间下的<Def>.php Action文件中。如果你需要改变这个规则，你需要使用自定义路由。

### 自定义路由
修改`config/route.php`文件配置你的自定义路由规则。
```php
return [
    'rules' => [
        'order/<id:\d+>' => 'order/info',
    ],
];
```
上述路由规则会将order/12345的请求路由到order/info?id=12345。


### 默认首页
框架默认首页为`home/index`，如果需要改成其他页面，则需要修改route的default属性；下述配置将默认首页改成`post/index`。
```
return [
    'default' => 'post',
    'rules' => [
        'order/<id:\d+>' => 'order/info',
    ],
];
```