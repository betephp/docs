# Hello World!

本文创建一个请求URL地址为hello/world的Web页面，展示内容为'Hello world!'。为了完成这个目标，我们需要创建一个Web Controller和一个视图文件。

### 创建Web Controller
为了创建`say/hello`请求的Web Action，可以在`app/Web/Say`下新建`Hello.php`来完成，也可以通过下面的命令行代码生成工具来完成。

```bash
./bete make:web Hello
```

上述命令将建立`app/Web/HelloController.php`文件，内容如下：

```php
<?php
 
 namespace App\Web;
 
 use App\Web\Controller;
 use Bete\Web\Request;
 
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
 
namespace App\Web;

use App\Web\Controller;
use Bete\Web\Request;

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
