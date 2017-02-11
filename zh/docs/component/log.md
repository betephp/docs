# 日志
日志是记录应用程序运行情况的重要工具，KanaPHP日志组件包含的日志记录和数据打点两个功能。

## 配置


## 日志记录
日志记录分为debug, info, notice, warning, error五个级别，通过以下方法调用。
```php
app()->log->debug('some thing hanppen');
app()->log->info();
app()->log->notice();
app()->log->warning();
app()->log->error();
```

## 数据打点
通常应用在上线运行后，我们需要知道一个页面访问了多少次，一个按钮被点击了多少次，日志组件提供了`data()`方法单独记录业务数据，数据放在`runtime/log/app.dat`文件中。

```php
app()->log->data('event_name', $extraData);
```