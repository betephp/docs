#Session

由于HTTP是无状态的，而Session允许应用程序在多个请求间共享数据。BetePHP将Session操作封装统一的API，并且支持文件、数据库、Redis等多种存储方式。

### 配置
Session的配置文件存储在```config/session.php```中，


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

### Flash Data
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


## Cookie