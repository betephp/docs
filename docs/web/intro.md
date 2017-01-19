# Web

BetePHP将应用运行模式分为Web和Console，Web模式用于处理用户的Web请求，Console用于通过命令行使用应用。

BetePHP处理一个典型的Web请求通常经过Route、Middleware、Action、Model、View这几层，如下所示：
![Screenshot](/img/process.png)

1. 用户请求一个URL，框架根据路由配置，将请求转发到具体的Action。
2. 在执行Action具体逻辑前，框架会根据Middleware配置，先执行与Action关联的Middleware。
3. Middleware通过后，则会开始执行Action的run方法，执行具体的业务逻辑；
4. run方法包含的具体业务逻辑则通过调用Model的方法来实现；
5. Model执行完业务逻辑后，将处理结果返回Action；
6. Action通过View组件渲染结果数据；
7. 然后将渲染后的页面返回给用户，完成请求。

## Web路由

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

## 中间件
中间件提供了一种方式让你的应用在执行具体业务逻辑前执行一段逻辑，在业务是否处理某个请求，比如你的一个接口需要用户登录才能访问，你可以给这个请求配置一个登录验证的中间件，通过登陆验证中间件，登录的用户将可以继续执行接下来的逻辑，未登录的用户则返回错误信息。

### 创建中间件
为了新建UserAuth中间件，在```app\Middleware```下建立```UserAuth.php```文件，内容如下：
```php
<?php

namespace App\Middleware;

use Bete\Foundation\Middleware;

class UserAuth extends Middleware
{
    public function beforeAction($action)
    {
        // todo implement check user auth logic
        if (!$isAuth) {
            app()->request->redirect('/');
        }
    }

    public function afterAction($action, $result)
    {
        return $result;
    }
}
```
beforeAction将会在Action执行之前运行，afterAction将会在Action执行完成后执行。

### 配置中间件

#### 全局配置
如果需要全局配置整个应用的中间件规则，可以在```config/middleware.php```中配置定义。
```php
<?php

return [
    'App\Middleware\CheckSign' => '*',
    'App\Middleware\UserAuth' => [
        'order/list,info',
    ],
];

```
上面的说明了CheckSign中间件将所有接口，而UserAuth中间件将用于order/list、order/info接口。

#### Action配置
全局配置用户批量配置中间件，有时你需要特别指定单个借口使用某个中间件，你可以在接口所在Action中定义Middleware方法，方法中定义该Action需要使用的中间件。
```php
<?php

namespace App\Http\Home;

use Bete\Http\Action;

class Index extends Action
{
    public $renderType = self::TYPE_HTML;

    public function middlewares()
    {
        return [
            'App\Middleware\PageCache',
        ];
    }

    public function run($request)
    {
        //todo ...
    }

}
```


## 请求响应处理

### 请求参数
获取请求参数，你可以使用request服务的get()、post()方法，他们将返回$_GET、$_POST内容：
```
$request = app()->request;

// equivalent to $get = $_GET;
$get = $request->get('name');

// equivalent to $name = isset($_GET['name']) ? $_GET['name'] : null;
$name = $request->get('name');

```

### 请求方法
```
$request = app()->request;

$request->isGet();
$request->isPost();
```

### 请求URL
```
$request = app()->request;

$request->isGet();
$request->isPost();
```