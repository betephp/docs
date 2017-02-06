# 安装

## 环境要求
* PHP >= 5.4.0
* PDO扩展
* OpenSSL扩展
* MbString扩展

## 安装


### 使用composer安装

```bash
composer create-project --prefer-dist betephp/betephp myproject
```

### 下载release包安装
打开下面其中一个release包下载页面，选择最新release版本包下载，解压下载的压缩包：

```
http://git.oschina.net/betephp/betephp/releases
```

进入项目根目录（下文未特殊注明，目录起始位置均为此根目录）

```bash
cd myproject #进入项目根目录
```

## 配置
### 建立app.ini配置文件
复制app.ini.example为app.ini，修改app.ini环境变量、数据库连接等适配当前环境；

```bash
cd config
cp app.ini.example app.ini
```

### 修改runtime文件夹权限
```bash
chmod -R 777 runtime/
```

## 运行
### 使用PHP内置Server启动App
```bash
cd public
php -S yourhost:9090
```

## 验证
在浏览器打开`http://yourhost:9090`，验证是否出现欢迎使用BetePHP页面。

## Web服务器配置
通常BetePHP是运行在PHP与Nignx/Apache组成的环境下。推荐的Nginx/Apache配置如下：

### Nginx配置
将Nginx的root设置为public目录，在nginx配置添加如下配置：

```
server {
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
}
```

### Apache配置
将Apache的DocumentRoot设置为项目的public目录，同时确保Apache开启了```mod_rewrite```。

