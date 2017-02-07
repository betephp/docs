# Web

BetePHP将应用运行模式分为Web和Console，Web模式用于处理用户的Web请求，Console用于通过命令行来使用应用。

BetePHP处理一个典型的Web请求通常经过Route、Middleware、Controller、Model、View这几层，如下所示：
![Screenshot](/img/process.png)

1. 用户请求一个URL，框架根据路由配置，将请求转发到具体的Action。
2. 在执行Action具体逻辑前，框架会根据Middleware配置，先执行与Action关联的Middleware。
3. Middleware通过后，则会开始执行Action的run方法，执行具体的业务逻辑；
4. run方法包含的具体业务逻辑则通过调用Model的方法来实现；
5. Model执行完业务逻辑后，将处理结果返回Action；
6. Action通过View组件渲染结果数据；
7. 然后将渲染后的页面返回给用户，完成请求。

## 路由

默认情况下，框架会将`abc/def`的请求路由到App\Web\AbcController的actionDef方法。Action文件中。如果你需要改变这个规则，你需要在路由层配置自定义路由规则。

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
通常，我们需要在用户访问某页面前检查用户是否登录，如果每个页面都写一段登录逻辑就会出现冗余，使用中间件，你可以将登录逻辑封装到中间件内，然后在Controller内针对每个页面接口单独配置。

### 创建中间件
为了新建CheckLogin中间件，在```app\Middleware```下建立```CheckLogin.php```文件，内容如下：

```php
<?php

namespace App\Middleware;

use Bete\Foundation\Middleware;

class CheckLogin extends Middleware
{
    public function beforeAction()
    {
        // todo implement check user auth logic
        if (!$isAuth) {
            app()->request->redirect('/');
        }
    }

    public function afterAction($result)
    {
        return $result;
    }
}
```

其中beforeAction将会在action执行之前运行，afterAction将会在action执行完成后执行。

### 配置中间件

你可以在Controller定义middlewares属性配置中间件。

```php

<?php
 
namespace App\Web;

use Bete\Web\Request;

class ExampleController extends Controller
{
    public $middlewares = [
        'CheckToken' => '*',
        'CheckCsrf' => 'register, login',
        'CheckLogin' => '* - index',
    ];
}
```

上述配置为example的所有action添加了CheckToken中间件；为register, login添加了CheckCsrf中间件，为除了index以外的action添加了CheckLogin中间件。

## Controller
一个请求具体的业务逻辑定义在Controller的action方法内。如下所示：

```php
<?php

namespace App\Web;

use Bete\Web\Request;

class ExampleController extends Controller
{
    public $layout = 'main';

    public $middlewares = [
        'CheckLogin' => 'middleware,list - list',
    ];

    public function actionIndex(Request $request)
    {
        return 'This is index action.';
    }
}
```


## 请求相应处理

### 请求处理
你可以使用Request对象的`get()`、`post()`方法获取请求的GET/POST参数，为了判断请求是GET还是POST请求，可以通过`isGet()`、`isPost()`判断。

```php
public function actionIndex(Request $request)
{
    $name = $request->get('name');
    $birthday = $request->post('birthday');

    if ($request->isPost()) { // if post request
        // ...
    }
}
```

### 响应处理
你可以通过response组件来刷新页面或者重定向页面，

```php
public function actionIndex(Request $request)
{
    app()->response->redirect('/');
    app()->response->refresh();
}
```
