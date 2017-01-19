# 预览

## 目录结构
```
app                             # App命名空间目录
    Console                     # 包含命令行Action
        Blog/DailyUpdate.php    # ./bete blog:dailyUpdate
    Exception                   # 包含用户自定义异常
    Http                        # 包含Http Action
        Home/Index.php          # http://localhost/home/index
    Middleware                  # 中间件文件夹
    Model                       # 存放业务Model
    view                        # 包含普通视图和布局视图
bootstrap                       # bootstrap
    app.php                     # app.php
config                          # 包含应用配置信息
    app.ini                     # 配置映射文件
    app.php                     # app配置文件
    database.php                # 数据库配置文件
    middleware.php              # 中间件配置文件
    redis.php                   # Redis配置文件
    route.php                   # 路由配置文件
    session.php                 # Session配置文件
public                          # 应用web root, 包含公开访问的内容
    index.php                   # 应用http入口
runtime                         # runtime目录，包含程序运行期间生成的文件
    compiled                    # 编译文件目录
    log                         # 日志目录
    session                     # 文件session目录
vendor                          # composer vender
```


## 代码生成工具
为了减少新建类时代码复制等重复工作，BetePHP使用命令行简化创建Model、中间件、Action的工作；

```bash
# 创建User Model
./bete make:model User

# 创建CheckToken中间件
./bete make:middleware CheckToken

# 创建接口为order/info的HTTP接口
./bete make:http order/info

# 创建order:dailyUpdate定时任务
./bete make:console order:dailyUpdate
```

## 接口预览
虽然BetePHP将命名空间尽量简化，使用一个类时还是需要知道类位于哪个命名空间。因此引入应用component，将常用功能封装成一个个的组件，然后通过```app()```作为入口访问，常用组件及API如下：

```php
# log
app()->log->info('some thing hanppen', $extraInfo);
app()->log->notice();
app()->log->warning();
app()->log->error();
app()->log->data('event_name', $data); # 业务日志打点

# cookie
app()->cookie->set(); # 默认加密，防止客户端修改
app()->cookie->get();

# session
app()->session->set();
app()->session->get();

# 数据库
app()->db->table('user')->where('id', 1)->first();
app()->db->table('order')->where('type', '=' 1)->all();

# 加密
app()->encrypter->encrypt($data);
app()->encrypter->decrypt($data);

# Redis
app()->redis->set();
app()->redis->get();

# 验证
$post = $request->post();
$rules = [
    'title' => 'required|string|between:5,50|name:标题',
    'content' => 'required|string|name:内容',
    'mobile' => 'required|mobile|name:手机号码',
    'email' => 'required|email|name:邮箱地址',
];
app()->validator->validate($post, $rules);
```
