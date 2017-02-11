# Validation

## Auto-validate

BetePHP offer validator to validate the input data. You can call `app()->validator` to use validator. For instance, to validate the post data from a form, we may write the below code:

```php
public function actionValidation(Request $request)
{
    if ($request->isPost()) {
        $data = $request->post();
        $rules = [
            'name' => 'required|chinese|between:2,20',
            'email' => 'required|email',
        ];

        app()->validator->validate($data, $rules);

        app()->session->setFlash('message', 'Validate success!');

        app()->response->redirect('/example/validation');
    }

    return $this->render('validation');
}
```

### Display error messages
If the validation is failed, the corresponding error message will be return. If the HTTP accept header is `application/json`, a json content will be display; In other case, the response will redirect to the previous page, and you can get the error messages by `$errors`:

```html
<form method="POST">

    <?php if (is_array($errors) && !empty($errors)) : ?>
    <div class="errors">
        <?php foreach ($errors as $key => $error) : ?>
            <p><?= $error ?></p>
        <?php endforeach; ?>
    </div>
    <?php endif; ?>

    <div><input type="text" class="input-text" name="name" placeholder="Username"></div>
    <div><input type="text" class="input-text" name="email" placeholder="Email"></div>
    <div><input type="submit" class="input-submit" name="sub" value="Submit"></div>

</form>
```

In some case, you may change the validated field name in the error message, you can add `name:` rule.

```php
$rules = [
    'name' => 'required|chinese|between:2,20|name:Username',
    'email' => 'required|email|name:Email',
];
```

## Validate manually

Sometime, you may want to custom error message when validataion is failed, The `make` method of validator will generate a new validator instance:

```php
public function actionValidation(Request $request)
{
    if ($request->isPost()) {
        $data = $request->post();
        $rules = [
            'name' => 'required|chinese|between:2,20',
            'email' => 'required|email',
        ];

        $validator = app()->validator->make($data, $rules);

        if ($validator->fails()) {
            //todo display error message
        } else {
            //todo insert data to database
        }
    }
}
```

## Available Validation Rules

### after:date
The field must be a value after a given date.

### alpha
The field must be entirely alphabetic characters.

### alnum
he field may have alpha-numeric characters.

### alnum_dash
The field may have alpha-numeric characters, underscores.

### array
The field must be a PHP array.

### before:date
The field must be a value preceding the given date.

### between:min,max
The field must have a size between the given min and max. 

### boolean
The field must be 0 or 1.

### chinese
The field must be chinese string.

### date
The field must be a valid date according to the strtotime PHP function.

### date_format:format
The field must match the given format. 

### different:field
The field must have a different value than field.

### digits:value
The field must be numeric and must have an exact length of value.

### digits_between:min,max
The field must have a length between the given min and max.

### email
The field must be formatted as an e-mail address.

### in:a,b,c,...
The field must be included in the given list of values.

### integer
The field must be an integer.

### ip
The field must be an IP address.

### json
The field must be a valid JSON string.

### max:value
The field must be less than or equal to a maximum value.

### min:value
The field must have a minimum value.

### not_in:a,b,c,...
The field must not be included in the given list of values.

### numeric
The field must be numeric.

### regex:pattern
The field must match the given regular expression.

### required
The field must be present in the input data.

### same:field
The given field must match the field 

### size:value
The field must have a size matching the given value. For string data, value corresponds to the number of characters. For numeric data, value corresponds to a given integer value. For an array, size corresponds to the count of the array.

### string
The field must be a string.

### url
The field must be a valid URL.
