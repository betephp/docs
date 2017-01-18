# 中间件
中间件提供了一种方式让配置你的应用是否处理某个请求，比如你的一个接口需要用户登录才能访问，你可以给这个请求配置一个登录验证的中间件，通过登陆验证中间件，登录的用户将可以继续执行接下来的逻辑，未登录的用户则返回错误信息。

## 创建中间件
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

## 配置中间件

### 全局配置
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

### Action配置
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