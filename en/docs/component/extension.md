# How to write your own component?

BetePHP offer some frequently-used component, but you can write your own component to fit your need.

## Steps
The section show you how to import Smarty library, and write smarty component for you app.

1. New `library` folder in your project root, download smarty release archieve, unzip it and move to library.

2. New `Component` folder in your app directory, create the `SmartyComponent.php`、`SmartyManager.php`:

```php
# SmartyComponent.php
<?php

namespace App\Component;

use Bete\Foundation\Component;

class SmartyComponent extends Component
{
    public function register()
    {
        $this->app->bind('smarty', function($app) {
            return new SmartyManager($app);
        });
    }

    public function names()
    {
        return ['smarty'];
    }
}

# SmartyManager.php
<?php

namespace App\Component;

use Bete\Foundation\Application;

class SmartyManager
{
    protected $app;

    protected $smarty;

    public function __construct(Application $app)
    {
        $this->app = $app;

        require_once($app->basePath() . '/library/smarty/libs/Smarty.class.php');

        $smarty = new \Smarty();

        $templateDir = $app->viewPath();
        $compileDir = $app->runtimePath() . '/smarty/templates_c/';
        $cacheDir = $app->runtimePath() . '/smarty/cache/';
        if (!file_exists($compileDir)) {
            mkdir($compileDir, 0777, true);
        }
        if (!file_exists($cacheDir)) {
            mkdir($cacheDir, 0777, true);
        }

        $smarty->setTemplateDir($templateDir);
        $smarty->setCompileDir($compileDir);
        $smarty->setCacheDir($cacheDir);

        $this->smarty = $smarty;
    }

    public function render($view, $data = [])
    {
        $this->smarty->clearAllAssign();

        $this->smarty->assign($data);

        $template = $this->getTemplateFile($view);

        return $this->smarty->display($template);
    }

    public function getTemplateFile($view)
    {
        return "{$view}.tpl";
    }
}
```

3. Now you have your own component, you need to configure it before using it. Open `config/app.php`, add it to components filed.

```php
return [
    # ...,
    'components' => [
        'Bete\Database\DatabaseComponent',
        'Bete\Validation\ValidationComponent',
        'Bete\View\ViewComponent',
        'Bete\Redis\RedisComponent',
        'Bete\Cookie\CookieComponent',
        'Bete\Session\SessionComponent',
        'App\Component\SmartyComponent',
    ],
    ...
];
```

4. That's all, you can use smarty component to render your view right now.

```php
class Index extends Action
{
    public function run(Request $request)
    {
        return app()->smarty->render('home/smarty', ['name' => 'BetePHP']);
    }
}
```
