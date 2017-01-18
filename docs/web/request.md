## 请求

### 请求参数
获取请求参数，你可以使用request服务的get()、post()方法，他们将返回$_GET、$_POST内容：
```
$request = app()->request;

// equivalent to $get = $_GET;
$get = $request->get('name');

// equivalent to $name = isset($_GET['name']) ? $_GET['name'] : null;
$name = $request->get('name');

```

### 请求方法
```
$request = app()->request;

$request->isGet();
$request->isPost();
```

### 请求URL
```
$request = app()->request;

$request->isGet();
$request->isPost();
```