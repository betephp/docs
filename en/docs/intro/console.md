# Console

If you need to process some task periodically, the console mode is what you need.

## Controller
Similar to http mode, the main logic in console mode is defined in the `action{Name}` method of `App\Console\{Name}Controller`, see below:

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

## Request
Similar to http, you need get some parameters when execute a command, `Bete\Console\Request`'s `param()`, `option()` is your tools, you can get paramter and option when execute a command:

```php
class ExampleController extends Controller
{
    public function index(Request $request)
    {
        return "Hello, this is index action.\n";
    }

    public function actionDailyUpdate(Request $request)
    {
        $status = $request->param(1); // Get the first paramter
        $time = $request->option('time'); // Get the time option
    }
}
```

When execute the below command, $status will be assigned to the first parameter, and $time will be assigned to the time option.

```bash
./bete example:dailyUpdate --time=3600 failed
```

## Code auto-generate

To reduce the repeated work of creating a class, BetePHP offer console tool to create model, middleware and controller.

```bash
./bete make:model UserFeedback
./bete make:middleware CheckToken
./bete make:http User
./bete make:console Task
```
