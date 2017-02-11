# Hello World!

This section introduce how to create a web page, and show 'Hello BetePHP!'. To achieve this goal, we need to create a Web Controller and a view.

## Creating Web Controller
First, we need to create HelloController(`app/Web/HelloController`), the below is the content:

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

## New actionWorld method
Second, we create the actionWorld method:

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
        $message = $request->get('message');

        return $this->render('say', ['message' => $message]);
    }   
 }
```

## Creating a view
View is responsible for display data. Last, you will create a `say` view that print the message parameter received from the action method:

```php
<?php
Hello <?= $message ?>!
```

This file should be saved in `view/hello/say.php`.

## Run
Open `http://yourhost/hello/say?message=BetePHP`, check if you can see 'Hello BetePHP!' in the page.
