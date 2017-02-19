# Hello World!

本文创建一个请求URL地址为hello/world的Http页面，展示内容为'Hello world!'。为了完成这个目标，我们需要创建一个Http Controller和一个视图文件。

### 创建Http Controller
为了创建`say/hello`请求的Http Action，可以在`app/Http/Say`下新建`Hello.php`来完成，也可以通过下面的命令行代码生成工具来完成。

```bash
./bete make:web Hello
```

上述命令将建立`app/Http/HelloController.php`文件，内容如下：

```php
<?php
 
 namespace App\Http;
 
 use App\Http\Controller;
 use Bete\Http\Request;
 
 class HelloController extends Controller
 {
     public function actionIndex(Request $request)
     {
         return "This is index action.";
     }
 }
```

### 创建actionWorld方法

我们新建一个actionWorld方法，此时HelloController代码如下：

```php
<?php
 
namespace App\Http;

use App\Http\Controller;
use Bete\Http\Request;

class HelloController extends Controller
{
    public function actionIndex(Request $request)
    {
        return "This is index action.";
    }

    public function actionWorld(Request $request)
    {
        return 'Hello world!';
    }   
 }
```

这时你打开`http://yourhost/hello/world`，将看到页面展示'Hello world!'。
