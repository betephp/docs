# Console

命令行是另一种运行应用程序的方式，当你的应用需要每天定时执行，你将用到命令行模式。BetePHP将命令行抽象成Console Action。

## 请求处理

```
./bete order:dailyUpdate --time=3600 failed
```

以上命令访问的就是```app/Console/Order/DailyUpdate.php```这个Console Action。你可以通过下述代码获取命令行的可选项以及参数。

```php
<?php

namespace App\Console\Order;

use Bete\Console\Action;
use Bete\Console\Request;

class DailyUpdate extends Action
{
    public function run(Request $request)
    {
        $status = $request->param(1); //获取第一个参数
        $time = $request->option('time'); //获取名为time的可选项
        return "Hello, Order:DailyUpdate.\n";
    }
}
```

## 代码自动生成

为了减少重复代码编写的时间，BetePHP支持Model、Middleware、Web Action、Console Action代码的自动生成。

```bash
./bete make:model UserFeedback
./bete make:middleware CheckToken
./bete make:web user/feedback
./bete make:console blog:dailyUpdate
```
