# Log

Log is used for logging some data when app is running.

## Log
The log provides the five logging levels: debug, info, notice, warning, error.

```php
app()->log->debug('some thing hanppen');
app()->log->info();
app()->log->notice();
app()->log->warning();
app()->log->error();
```

## Data

When running a website, we need to know how many times a page is visited, how many times a button is clicked. Log offer `data()` method to log some important data separately, and the log data is saved at `runtime/log/app.dat`.

```php
app()->log->data('event_name', $extraData);
```
