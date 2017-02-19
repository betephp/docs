# Http

You can run BetePHP app in two ways: Http and Console, Http is used for handling web page or api request, and Console is used for access throught console command.

The process for handling Http request include Route, Middleware, Controller Action, Model and View, see below:
![Screenshot](/img/process.png)

1. A user make a url request;
2. The route determine which controller/action is responsible for this request;
3. Before run the action, some middleware will execute according to the controller middleware configure;
4. When run action, it will call model, and get some data from database;
5. Fetch data from model;
6. Action will render view with the data receive from model;
7. Last, print the rendered content to user;

## Route
In default configure, the `abc/edf` request will route to the `actionDef` method of `App\Http\AbcController`, if you want to change this rule in some case, you need to modify the route configure.

### Custom route
Modify `config/route.php` to configure your custom route rule:

```php
return [
    'rules' => [
        'order/<id:\d+>' => 'order/info',
    ],
];
```

The above configure will redirect the `order/12345` request to `order/info?id=12345`.

### Default Home
The default home page is `home/index`, if you want to change it to other page, you need to modify the default attribute of route, the below configure change home page to `post/index`.

```
return [
    'default' => 'post',

    'rules' => [
        'order/<id:\d+>' => 'order/info',
    ],
];
```

## Middleware
In some case, we need check-login before access a web page, if you write the check-login code in each page, it will make a lot of repeated code. Using the middleware, you can write your check-login code in a middleware, and configure it in the controller for each action.

### Create a middleware
To create a CheckLogin middleware, new a `app/Middleware/CheckLogin.php` file, the content is below:

```php
<?php

namespace App\Middleware;

use Bete\Foundation\Middleware;

class CheckLogin extends Middleware
{
    public function beforeAction()
    {
        // todo implement check user login
        if (!$isLogin) {
            app()->request->redirect('/');
        }
    }

    public function afterAction($result)
    {
        return $result;
    }
}
```

The beforeAction method will execute before action, and the afterAction method will execute after action.

### Configure middleware

You can configure middleware throught define the middlewares attribute of the controller:

```php

<?php
 
namespace App\Http;

use Bete\Http\Request;

class ExampleController extends Controller
{
    public $middlewares = [
        'CheckToken' => '*',
        'CheckCsrf' => 'register, login',
        'CheckLogin' => '* - index',
    ];
}
```

The above configure include: CheckToken Middleware will be added for all the actions, CheckCsrf will be added for register and login action, CheckLogin will be added for all the actions except index.

## Controller
A http request 
The main logic for a http request is defined in the `action{Name}` method of `App\Http\{Name}Controller`, see below:

```php
<?php

namespace App\Http;

use Bete\Http\Request;

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

## Request and Response

### Request
You can use the `get()` and `post()` method of `Request` to get GET/POST data, to determine the request method, you can use `isGet()`, `isPost`,

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

### Response
You can use response component to refresh page or redirect.

```php
public function actionIndex(Request $request)
{
    app()->response->redirect('/');
    app()->response->refresh();
}
```
