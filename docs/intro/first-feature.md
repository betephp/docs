# Hello World!
该部分创建一个请求URL地址为say/hello的Web页面，展示内容为'Hello world!'。为了完成这个目标，我们需要创建一个Web Action和一个视图文件。

### 创建Web Action
为了创建`say/hello`请求的Web Action，可以在`app/Web/Say`下新建`Hello.php`来完成，也可以通过下面的命令行代码生成工具来完成。

```bash
./bete make:web say/hello
```

上述命令将建立`app/Web/Say/Hello.php`文件，内容如下：

```php
<?php

namespace App\Web\Say;

use Bete\Web\Action;
use Bete\Web\Request;

class Hello extends Action
{

    public $renderType = self::TYPE_HTML;

    public function middlewares()
    {
        return [];
    }

    public function run(Request $request)
    {
        return "Hello, Say/Hello.";
    }

}
```

这时你打开`http://yourhost/say/hello`，将看到页面展示'Hello, Say/Hello.'。

我们继续下一步，我们需要显示'Hello world!'，这里我们Hello就通过视图展现，World则通过Action的变量传递给视图。因为需要用视图渲染页面，并且需要传递变凉给视图，我们需要用到Action的`render()`，`render()`方法第一个参数是具体的视图文件，第二个参数则是传递变量组成的数据。更改后的Action如下：

```php
<?php

namespace App\Web\Say;

use Bete\Web\Action;
use Bete\Web\Request;

class Hello extends Action
{

    public $renderType = self::TYPE_HTML;

    public function middlewares()
    {
        return [];
    }

    public function run(Request $request)
    {
        return $this->render('say/hello', ['name' => 'world']);
    }

}
```

### 创建视图
然后新建`app/view/say/hello.php`的视图文件，内容如下：

```php
Hello <?= $name ?>.
```

这时打开`http://yourhost/say/hello`，查看页面是否显示'Hello world!'。
