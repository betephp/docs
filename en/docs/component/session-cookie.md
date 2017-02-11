#Session

Session and cookie allow data be persisted across multiple user requests.

### Configure
The Session configure is saved at `config/session.php`. You can configure storage driver, lifetime in here:

```
return [

    'driver' => ini('SESSION_DRIVER', 'file'), //file, database, redis

    'lifetime' => 7200, // life time

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


### Usage

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
Flash Session is used for storage session data only for the next reqeust.

```
// get Flash Session
$value = app()->session->getFlash('message');

// set Flash Session
app()->session->setFlash('message', 'Save success');

// delete Flash Session
app()->session->removeFlash('message');

// clear all the Flash Session
app()->session->clearFlash();
```


## Cookie
```
app()->cookie->set('source_id', 'baidu', 3600);

app()->cookie->get('source_id');
```
