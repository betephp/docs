# Overview

## Directory construction

```
app                             # App namespace directory
    Console                     # Include all console controller
        ExampleController.php   # Console ExampleController
    Exception                   # Include user custom exception and exception handler
    Web                         # Include all web controller
        ExampleController.php   # Web ExampleController
    Middleware                  # Middleware
    Model                       # Model
bootstrap                       # bootstrap
    app.php                     # app.php
config                          # Inlcude all app configure
    app.ini                     # Environment variable configure
    app.php                     # App configure
    database.php                # Database configure
    redis.php                   # Redis configure
    route.php                   # Route configure
    session.php                 # Session configure
public                          # Web root, include all access resource in public
    index.php                   # index.php
runtime                         # Runtime directory, include some temporary file in runtime
    compiled                    # Compiled
    log                         # Log
    session                     # Session
vendor                          # composer vender
view                            # Include view, layout files
```


## Code generate tool
For reduce repeat work on creating new classs, BetePHP offer console tool to simplify the work for creating Model, Controller and Middleware:

```bash
# New User Model
./bete make:model User

# New CheckToken Middleware
./bete make:middleware CheckToken

# New Web Controller
./bete make:web Order

# New Console Controller
./bete make:console Task
```

## API overview
Although Betephp's namespace is very straightforward, we still offer a way to use component more simply.

```php
# log
app()->log->info('some thing hanppen', $extraInfo);
app()->log->notice();
app()->log->warning();
app()->log->error();
app()->log->data('event_name', $data); # Biz log

# cookie
app()->cookie->set();
app()->cookie->get();

# session
app()->session->set();
app()->session->get();

# Database
app()->db->table('user')->where('id', 1)->first();
app()->db->table('order')->where('type', '=' 1)->all();

# Redis
app()->redis->set();
app()->redis->get();

# Validator
$post = $request->post();
$rules = [
    'title' => 'required|string|between:5,50|name:Title',
    'content' => 'required|string|name:Content',
    'email' => 'required|email|name:Email',
];
app()->validator->validate($post, $rules);
```
