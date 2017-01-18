# 开发第一个接口

## 用户反馈功能
功能：用户填写一个表单，提交反馈信息，如果输入信息错误，提示错误消息，正确则把内容保存到数据库；


## 准备数据表


## 配置数据库


## 创建一个Feedback Model
```
./bete make:model Feedback
```

## 创建一个Web Action
```
./bete make:web user/feedback
```

##
在```app/view```目录下新建```user/feedback.php```文件，包含下面内容：
```
<!DOCTYPE html>
<html>
<head>
    <title><?= $this->title ?></title>
</head>
<body>

<?php foreach ($errors as $error) : ?>
    <div><?= $error; ?></div>
<?php endforeach; ?>

<form method="POST" id="reg">
    <input type="text" name="username" id="username">
    <input type="password" name="mobile" id="mobile">
    <input type="submit" name="sub" id="sub1" value="Submit">
</form>
</body>
</html>
```


## 运行
在浏览器打开```http://localhost:9090/user/feedback```，查看效果。