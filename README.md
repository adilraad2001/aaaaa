# aaaaa

<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html/base
    <Directory /var/www/html/base/>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

sudo a2ensite base.conf
sudo systemctl restart apache2

CREATE DATABASE base;
GRANT ALL PRIVILEGES ON base.* TO 'base_user'@'localhost' IDENTIFIED BY 'base_password';
FLUSH PRIVILEGES;
EXIT;

sudo cp /var/www/html/base/base_conf.php.dist /var/www/html/base/base_conf.php
sudo nano /var/www/html/base/base_conf.php

$BASE_urlpath = '/base';
$DBlib_path = '/var/www/html/base/lib';
$DBname = 'base';
$DBuser = 'base_user';
$DBpass = 'base_password';
$alert_dbname = 'snort';

sudo chown -R www-data:www-data /var/www/html/base
sudo chmod -R 755 /var/www/html/base
