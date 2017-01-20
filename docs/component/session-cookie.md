#Session

由于HTTP是无状态的，而Session允许应用程序在多个请求间共享数据。

### 配置
Session的配置文件位于`config/session.php`，可配置Session的存储方式和存活时间，存储方式可以选择文件、数据库或Redis，存活时间默认为2个小时。
```
return [

    'driver' => ini('SESSION_DRIVER', 'file'), //file, database, redis

    'lifetime' => 7200, // 存活时间

    'file' => [
        'path' => runtime_path('session'),
    ],

    'database' => [
        'connection' => 'default',
        'table' => 'session',
    ], 

    'redis' => [
        'connection' => 'default',
        'prefix' => 'session:',
    ],

];
```


### 使用
```
// get the session value for a key, if doesn't exist, return null
$value = app()->session->get('source_id');

// set a session variable
app()->session->set('language', 'en_US');

// delete a session variable
app()->session->remove('language');

// clear all the session variable
app()->session->clear();
```

### Flash Session
Flash Session用于存放仅在下一次请求有效的数据，这种数据通常用于表单提交后，重定向到另外一个页面显示表单处理结果。`validator`组件在数据校验失败重定向到表单提交页用到这种数据类型。使用方法如下所示：

```
// 获取Flash Session
$value = app()->session->getFlash('message');

// 设置Flash Session
app()->session->setFlash('message', 'Save success');

// 删除Flash Session
app()->session->removeFlash('message');

// 清除所有Flash Session
app()->session->clearFlash();
```


## Cookie
为了防止客户端修改，Cookie默认使用openssl加密，
```
app()->cookie->set('source_id', 'baidu', 3600);

app()->cookie->get('source_id');
```
