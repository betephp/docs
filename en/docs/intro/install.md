# Install

## Environment
* PHP >= 5.4.0
* PDO extension
* OpenSSL extension
* MbString extension

## Install

You can install BetePHP by composer or just download release achive.

### Install with Composer

```bash
composer create-project --prefer-dist betephp/betephp myproject
```

### Install with downloading release archive
Open the below release page, and choose the latest `release.zip` to download:

```
https://github.com/betephp/betephp/releases
```

Enter project root: (The inital directory of operation is the project root if we don't illustrate especially)

```bash
cd myproject
```

## Configure
### New app.ini file
Copy app.ini.example to app.ini, edit environment variable in app.ini to fit your environment.

```bash
cd config
cp app.ini.example app.ini
```

### Modify runtime folder permission

```bash
chmod -R 777 runtime/
```

## Run
You can run App with Apache+PHP, Nginx+PHP, or just use PHP build-in server.

### Run with PHP build-in server:

```bash
cd public
php -S yourhost:9090
```

## Check if the installation is success
Open`http://yourhost:9090` web page, check if there is BetePHP welcome message in the page.

## Web server configure
Normally, BetePHP run with Nginx+PHP or Apache+PHP, see below for the recommended Nginx, Apache:

### Nginx configure
Set nginx root to public directory, and add the below configure:

```
server {
    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }
}
```

### Apache configure
Set Apache document root to public directory, and make sure Apache enable ```mod_rewrite```.

