# 验证

## 自动验证

BetePHP提供validator组件来验证输入数据。你可以调用`app()->validator`来使用validator组件。比如要验证表单POST提交的用户信息，我们可以在Action的run方法中定义如下逻辑来验证。

```php
public function run(Request $request)
{
    if ($request->isPost()) {
        $data = $request->post();
        $rules = [
            'name' => 'required|chinese|between:2,20',
            'mobile' => 'required|mobile',
            'email' => 'required|email',
        ];

        app()->validator->validate($data, $rules);
    }
}
```

如果请求的POST数据校验通过，Action会继续进行接下来的逻辑，如果校验失败，框架则会根据请求头做相应的相应。如果POST请求的HTTP Header头指定了`Accept: application/json`，将会自动输出一段带有校验失败信息的json数据，否则则会跳转到表单提交页，并将错误信自动赋值给视图文件的`$errors`变量。

```html
<form method="POST">

    <?php if (is_array($errors) && !empty($errors)) : ?>
    <div class="errors">
        <?php foreach ($errors as $key => $error) : ?>
            <p><?= $error ?></p>
        <?php endforeach; ?>
    </div>
    <?php endif; ?>

    <div><input type="text" class="input-text" name="name" placeholder="姓名"></div>
    <div><input type="text" class="input-text" name="mobile" placeholder="手机"></div>
    <div><input type="text" class="input-text" name="email" placeholder="邮箱"></div>
    <div><input type="submit" class="input-submit" name="sub" value="提交"></div>

</form>
```

默认情况下显示的错误信息会是'name不能为空'、'email不是一个可用的邮箱地址'，如果你需要将字段名转成中文，你可以在验证规则定义时加上name规则，这样验证失败后，错误信息的字段名将被name:后的值替换。

```php
public function run(Request $request)
{
    if ($request->isPost()) {
        $data = $request->post();
        $rules = [
            'name' => 'required|chinese|between:2,20|name:姓名',
            'mobile' => 'required|mobile|name:手机号码',
            'email' => 'required|email|name:邮箱地址',
        ];

        app()->validator->validate($data, $rules);

        app()->session->setFlash('message', '验证成功');

        app()->response->redirect('/example/validation');
    }

    return $this->render('example/validation');
}
```

## 手动验证

## 可用的验证规则

### after:date
验证的字段必须是一个晚于date的日期，date必须是一个可用的日期

### alpha
验证的字段仅能包含字母

### alnum
验证的字段仅能包含字母、数字

### alnum_dash
验证的字段仅能包含字母、数字、下划线

### array
验证的字段必须是一个数组

### before
验证的字段必须是一个早于date的日期

### between:min,max
验证的字段大小必须介于min和max之间

### boolean
验证的字段必须是0或者1

### chinese
验证的字段仅能包含中文

### date
验证的字段必须是一个合法的日期

### date_format:format
验证的字段必须匹配format的日期格式

### different:field
验证的字段必须和filed字段值不相同

### digits:value
验证的字段必须是数字并且是value位数

### digits_between:min,max
验证的字段必须是数字并且位数是介于min和max之间

### email
验证的字段必须是一个可用的邮箱地址

### id_card
验证的字段必须是一个可用的身份证号码

### in:a,b,c,...
验证的字段必须是一个给出值的某一个

### integer
验证的字段必须是一个整型数字

### ip
验证的字段必须是一个合法的IP地址

### json
验证的字段必须是一个合法的JSON字符串

### max
验证的字段必须是一个可用的邮箱地址

### min
验证的字段必须是一个可用的邮箱地址

### mobile
验证的字段必须是一个可用的邮箱地址

### not_in
验证的字段必须是一个可用的邮箱地址

### numeric
验证的字段必须是一个可用的邮箱地址

### regex
验证的字段必须是一个可用的邮箱地址

### required
验证的字段必须是一个可用的邮箱地址

### same
验证的字段必须是一个可用的邮箱地址

### size
验证的字段必须是一个可用的邮箱地址

### string
验证的字段必须是一个可用的邮箱地址

### required
验证的字段必须是一个可用的邮箱地址

### 




### after:date
date必须是一个可用的日期




### after:date
date必须是一个可用的日期




### after:date
date必须是一个可用的日期







