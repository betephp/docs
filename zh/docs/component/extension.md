# 如何编写自己的组件
BetePHP提供的是常用的功能组件，用户可以根据需要编写自己的组件，还可以将自己的组件开源提供给其他BetePHP用户使用。

## 步骤
本文将smarty做为组件集成到BetePHP，说明如何编写BetePHP组件。

1.在项目根目录新建`library`目录，下载smarty发行包，解压重命名为smarty后放入`library`。

2.在`app`目录新建Component目录，在Component目录新建SmartyComponent.php、SmartyManager.php，内容如下：

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

3.组件开发完成后，需要配置才能使用，打开`config/app.php`，在components节点下添加`App\Component\SmartyComponent`：

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

4.这样你就可以在应用内使用smarty组件渲染视图了。

```php
class Index extends Action
{
    public function run(Request $request)
    {
        return app()->smarty->render('home/smarty', ['name' => 'BetePHP']);
    }
}
```
