# Console

如果你需要在后台按周期执行业务逻辑，你就需要用到Console模式。

## Controller
同Http模式类似，Console的具体的业务逻辑定义在App\Console\{Name}Controller的action{Name}方法内。如下所示：

```php
<?php

namespace App\Console;

use Bete\Console\Controller;
use Bete\Console\Request;

class ExampleController extends Controller
{
    public function index(Request $request)
    {
        return "Hello, this is index action.\n";
    }

    public function actionDailyUpdate(Request $request)
    {
        print_r($request->param()); 
        print_r($request->option());
    }
}
```

## 请求处理

Console模式下，有时需要根据传递过来的不同参数执行不同逻辑，通过Bete\Console\Request的`param()`, `option()`方法，你可以获取命令传递的参数、选项。

```php
class ExampleController extends Controller
{
    public function index(Request $request)
    {
        return "Hello, this is index action.\n";
    }

    public function actionDailyUpdate(Request $request)
    {
        $status = $request->param(1); //获取第一个参数
        $time = $request->option('time'); //获取名为time的可选项
    }
}
```

当执行下面的命令后，$status将赋值命令行传递的第一个参数值（'failed'），$time将赋值time选项值（'3600'）。

```bash
./bete example:dailyUpdate --time=3600 failed
```

## 代码自动生成

为了减少重复代码编写的时间，BetePHP支持Model、Middleware、Http Controller、Console Controller代码的自动生成。

```bash
./bete make:model UserFeedback
./bete make:middleware CheckToken
./bete make:http User
./bete make:console Task
```
