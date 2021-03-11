

## Requirements

* Tested only on Linux for now, MAC OS X & other unices should work, too
* PHP 5.4+ (see Quickstart below) & MySQL 5+
* PHP dependencies as mentioned below (gnupg etc.) must compile on your platform
* ImageMagick (`identify`, `convert`, `mogrify` executables must be in `PATH`)


## Quickstart
*These instructions are only suited for a quick & dirty setup for developers!*



### phpbrew (install php 5.4)
install phpbrew itself:

```bash
curl -L -O https://github.com/phpbrew/phpbrew/raw/master/phpbrew
chmod +x phpbrew
sudo mv phpbrew /usr/bin/phpbrew
```

install latest php 5.4 with minimal extensions (pdo, mysql, multibyte and PGP only required for now):

```bash
phpbrew install 5.4 +pdo +mb +mysql +gnupg +gmp
```

### composer
install extensions needed for composer:

```bash
phpbrew ext install json
phpbrew ext install filter
phpbrew ext install hash
phpbrew ext install ctype
```

install composer

```bash
phpbrew install-composer
```

### Application
clone repo from github (requires git):

```bash
git clone https://github.com/MatthiasWinzeler/scam.git
cd scam
```

install dependencies using composer

```bash
composer install
```

install MySQL (add a dedicated user for scam), then init database with the provided scripts:

```bash
for sql_file in app/install/*.sql; do mysql -uroot -p < $sql_file; done
```
```

### Configuration
Set the connection details for MySQL in `app/config/config.php`:
```php
define('DB_HOST', '127.0.0.1');
define('DB_NAME', 'scam');
define('DB_USER', 'your_mysql_user');
define('DB_PASS', 'your_mysql_password');
```

Now, you can run the server:

```bash
php -S localhost:3000
```

Access it with your webbrowser pointing to http://localhost:3000 or http://localhost:3000/?c=admin (admin interface)

## Developer notes
To debug, install xdebug and configure it for your favorite IDE:

```bash
phpbrew ext install xdebug stable
```
