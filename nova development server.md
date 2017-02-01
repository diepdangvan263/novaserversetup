#Introduction
If you're a Nova Framework developer planning on using the Mint Desktop as your development platform, then these steps well help you setup your system.

This is for a developer machine and not for a live environment!

These steps are for Mint (Sarah) 18.  The steps may work with Ubuntu 16.10, but I haven't tried it.

Install Mint 18 desktop using either the DVD or Thumb drive.  If you are using a SSD, I recommend you set the /home directory to a installed on a standard hard drive.


#Installation stack

* PHP Environment
    * [PHP5](#php5)
    * [PHP7](#php7)
    * [PEAR](#pear)
    * [Phing](#phing)
* General Environment
    * [git / github](#git)
    * [memcache](#memcache)
    * [mycrypt](#mycrypt)
    * [apache2](#apache2)
    * [nginx](#nginx)
    * [mysql](#mysql)
    * [mariadb](#mariadb)
    * [sqlite](#sqlite)
    * [gmagick](#gmagick)
    * [imagemagic](#imagemagic)
    * [curl](#curl)
    * [composer](#composer)
* PHP QA Environment
    * [PHP Codesniffer](#php-codesniffer)
    * [PHPUnit](#phpunit)
    * [PHP CS Fixer](#php-cs-fixer)
    * [PHP CS Beautifier](php-beautifier)
    * [Sublime Text 3](#sublime)
* Frontend Tools
    * [NodeJs + Grunt + Bower](#nodejs)
    * [PNG Tools for Iconizr](#iconizr)
* Utilities
    * [GitKraken GIT GUI](#kraken)
    * [PHPmyadmin](#phpmyadmin)
* Other
    * [php.ini settings](#php-ini)
    * [How to debug with XDebug and PHPStorm on Firefox and command line](#debugging-with-phpstorm)
    * [Apache2 config example](#apache2-config-example)
    * [Nginx config example](#nginx-config-example)

#Installation PHP Environment

Nova Framework will run with either PHP 5.6 or 7.0.  Depending on what your host provider
is running, choose that for your server.

<a name="php5"></a>
##PHP5
```shell
sudo apt-get install php5-cli php5-common php-apcu php-pear php-xdebug php5-curl php5 php5-dev \
php5-xsl php5-gd php5-imap php5-cli php5-cgi php5-json php5-tidy php5-zip \
php5-intl php5-mbstring php-gettext
```

<a name="php7"></a>
##PHP7.0
```shell
sudo apt-get install php7.0-cli php7.0-common php-apcu php-pear php-xdebug php7.0-curl php7.0 \
php7.0-xsl php7.0-gd php7.0-imap php7.0-cli php7.0-cgi php7.0-json php7.0-zip \
php7.0-intl php7.0-mbstring php7.0-tidy php7.0-dev php-gettext
```

<a name="pear"></a>
##PEAR
```shell
sudo apt-get install pear-channels
sudo pear upgrade PEAR
```

<a name="phing"></a>
##PHING
```shell
sudo apt-get install phing
```

#Install General Environment
<a name="git"></a>
##git
```shell
sudo apt-get install git-all
git config --global color.branch auto
git config --global color.diff auto
git config --global color.status auto

#Manual on how to install ssh keys on github http://help.github.com/linux-set-up-git/
```
<a name="memcache"></a>
##memcache
```shell
sudo apt-get install memcached
sudo apt-get install php-memcache
```
<a name="mcrypt"></a>
##mcrypt
```shell
sudo apt-get install mycrypt

for php5 use
sudo apt-get install php5-mcrypt

for php7 use
sudo apt-get install php7.0-mcrypt

```

<a name="apache2"></a>
##apache2
```shell
sudo apt-get install apache2 apache2-suexec-pristine libapache2-mod-php
sudo a2enmod suexec rewrite ssl actions include cgi
sudo a2enmod dav_fs dav auth_digest headers
```
**You should see the following question:**

*Web server to reconfigure automatically:*

Select apache2 and then ok.

<a name="nginx"></a>
##nginx
```shell
sudo apt-get install nginx

#for php5 use
sudo apt-get install php5-fpm

#edit listen port in /etc/php5/fpm/pool.d/www.conf
listen = 127.0.0.1:9009

sudo service php5-fpm restart

#for php7 use
sudo apt-get install php7.0-fpm

#edit listen port in /etc/php/7.0/fpm/pool.d/www.conf
listen = 127.0.0.1:9009

sudo service php7.0-fpm restart


#now restart nginx
sudo service nginx restart
```
You can run either mysql or mariadb as your database server.

<a name="mysql"></a>
##mysql
```shell
sudo apt-get install mysql-server mysql-client

#for php5 use:
sudo apt-get install php5-mysql

#for php7.0 use:
sudo apt-get install php7.0-mysql

```

<a name="mariadb"></a>
##mariaDB
```shell
sudo apt-get install mariadb-server mariadb-client

#for php5 use:
sudo apt-get install php5-mysql

#for php7.0 use:
sudo apt-get install php7.0-mysql

```

<a name="sqlite"></a>
##SQLite
```shell

#for php5 use
sudo apt-get install sqlite3 php5-sqlite

#comment in /etc/php/5.6/apache2/conf.d/20-sqlite3.ini
extension=sqlite3.so

#for php7.0 use
sudo apt-get install sqlite3 php7.0-sqlite

#comment in /etc/php/7.0/apache2/conf.d/20-sqlite3.ini
extension=sqlite3.so
```

<a name="gmagick"></a>
##gmagick
```shell
sudo apt-get install graphicsmagick libgraphicsmagick1-dev
sudo pecl install gmagick-beta

#for php5 use
#Create file /etc/php/5.6/apache2/conf.d/20-gmagick.ini and add a line
extension=gmagick.so

#for php7.0 use
#Create file /etc/php/7.0/apache2/conf.d/20-gmagick.ini and add a line
extension=gmagick.so
```

<a name="imagemagick"></a>
##imagemagick
```shell
sudo apt-get install imagemagick php-imagick

```

<a name="curl"></a>
##curl
```shell
sudo apt-get install curl
```

<a name="composer"></a>
##composer
```shell
sudo apt-get install composer
```

#Installation PHP QA Environment
<a name="php-codesniffer"></a>
##CodeSniffer
```shell
sudo pear install PHP_CodeSniffer
```

* README Symfony2 Coding Standard
    * [public](https://github.com/opensky/Symfony2-coding-standard)
    * [private](https://github.com/nzzdev/Symfony2-coding-standard/blob/master/README.md)

<a name="phpunit"></a>
##PHPUnit
```shell

```

<a name="php-cs-fixer"></a>
##php-cs-fixer
```shell
sudo wget http://cs.sensiolabs.org/get/php-cs-fixer.phar -O /usr/bin/php-cs-fixer
sudo chmod a+x /usr/bin/php-cs-fixer
```

<a name="phpstorm"></a>
##PHP Storm IDE
* Download and install PHP Storm - http://www.jetbrains.com/phpstorm/
* Install Sun JDK - http://www.webupd8.org/2012/01/install-oracle-java-jdk-7-in-ubuntu-via.html
* increase file watching limit (http://confluence.jetbrains.net/display/IDEADEV/Inotify+Watches+Limit)

```shell
#add line to /etc/sysctl.conf
fs.inotify.max_user_watches = 524288

#apply changes
sudo sysctl -p
```

#Frontend Tools
<a name="nodejs"></a>
##NodeJs + Grunt + Bower

```shell
# nodejs
sudo apt-get install python-software-properties
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install nodejs

#grunt
sudo npm install -g grunt-cli

#bower
sudo npm install -g bower
```

<a name="iconizr"></a>
##PNG Tools for Iconizr

```shell
# PNG Tools for Iconizr
sudo apt-get install pngcrush pngquant optipng
sudo apt-get install checkinstall
cd /tmp
wget http://downloads.sourceforge.net/project/optipng/OptiPNG/optipng-0.7.4/optipng-0.7.4.tar.gz
tar xvf optipng-0.7.4.tar.gz
cd optipng-0.7.4
./configure
make
sudo checkinstall
```
#Utilities

<a name="utilities"></a>
##GitKraken
*Git GUI*
```shell

```

##Phpmyadmin
*Mysql manager*
```shell
sudo apt-get install phpmyadmin
```



#Configuration

<a name="php-ini"></a>
##PHP
* Change this settings in /etc/php5/cli/php.ini for for *all webservers*
* Change this settings in /etc/php5/apache2/php.ini if you have installed *apache2*
* Change this settings in /etc/php5/fpm/php.ini if you have installed *nginx and fpm*

```shell
memory_limit = 512m
display_errors = On
html_errors = On
post_max_size = 32m
upload_max_filesize = 32m
default_charset = utf8

uncomment

extension=php_fileinfo.dll
extension=php_intl.dll
extension=php_openssl.dll

```

<a name="debugging-with-phpstorm"></a>
#Debugging with XDebug on Browser and Command line

The example is made for PHPStorm IDE with Apache2 webserver. But other IDE's or webservers should work in a similar way.

* Mint 18
  * with php-fpm -> `sudo ln -s /etc/php5/mods-available/xdebug.ini /etc/php5/fpm/conf.d/20-xdebug.ini`
  * with apache2 -> `sudo ln -s /etc/php5/mods-available/xdebug.ini /etc/php5/apache2/conf.d/20-xdebug.ini`
  * with cli -> `sudo ln -s /etc/php5/mods-available/xdebug.ini /etc/php5/cli/conf.d/20-xdebug.ini`
  * Edit /etc/php5/mods-available/xdebug.ini

##Configuration
```shell
#Edit xdebug.ini
xdebug.remote_enable=On
xdebug.remote_host=localhost
xdebug.remote_port=9002
xdebug.remote_handler=dbgp
xdebug.profiler_append=Off
xdebug.profiler_enable=Off
xdebug.profiler_enable_trigger=Off
xdebug.profiler_output_dir="/tmp/kcachegrind"
xdebug.max_nesting_level = 1000

sudo service apache2 restart

#Add to /home/<your_username>/.bashrc
export XDEBUG_CONFIG="PHPSTORM";

#reload bash settings
source ~/.bashrc
```
* Edit Settings in PHPStorm
    * Go to File->Settings->PHP->Debug
    * Change XDebug Debug Port to 9002
* Install Easy XDebug Plugin for Firefox
    * https://addons.mozilla.org/de/firefox/addon/easy-xdebug/

##Debugging via Firefox
* Firefox: Click on ‘StartXDebug Session’ Symbol on bottom right
* PHPStorm: Click on Run->Start Listen PHP Debug Connections
* PHPStorm: Set a breakpoint and do call via firefox browser

##Debugging via Console
* PHPStorm: Click on Run->Start Listen PHP Debug Connections
* Set a breakpoint and run a console command

#for PHPUnit Skeleton Generator add phpunit-skelgen under file->settings->ProjectSettings->PHP->PHPUnit->SkeletonGenerator
#Usually it's stored in
/usr/bin/phpunit-skelgen
```

/usr/bin/phpunit-skelgen


<a name="apache2-config-example"></a>
#Apache2 config example (with Symfony2 framework)
Assume you want to have your project in `/home/username/my_webside`

```shell
# Change user/group of Apache2
# edit /etc/apache2/apache2.conf
User <username>
Group <usergroup>

#Add entry to /etc/hosts
127.0.0.1 www.my_webside.lo

#Create file
/etc/apache2/sites-available/www.my_webside.lo

#edit file (with example config)
<VirtualHost *:80>
    ServerName  www.my_webside.lo
    DocumentRoot /home/username/my_webside/web
    ErrorLog ${APACHE_LOG_DIR}/www.my_webside.lo.error.log
    CustomLog ${APACHE_LOG_DIR}/www.my_webside.lo.access.log common
</VirtualHost>

#create symbolic link to enable a site
sudo ln -s /etc/apache2/sites-available/www.my_webside.lo /etc/apache2/sites-enabled/www.my_webside.lo

#restart apache
sudo /etc/init.d/apache2 restart
```

<a name="nginx-config-example"></a>
#Nginx config example (with Symfony2 framework)
Assume you want to have your project in `/home/username/my_webside`

```shell
# Change user of Nginx
# edit /etc/nginx/nginx.conf
User <username>

# Change user of php5-fpm
# edit /etc/php5/fpm/pool.d/www.conf
user = <username>
group = <group of user>

#Add entry to /etc/hosts
127.0.0.1 www.my_webside.lo

#Create file
/etc/nginx/sites-available/www.my_webside.lo

#edit file (with example config)
#www.my_webside.lo
server {
    listen 80;
    server_name www.my_webside.lo;

    access_log  /var/log/nginx/www.my_webside.lo.log;

    location / {
        root /home/username/my_webside/web;
        index  index.html index.htm index.php app_dev.php;
        if ($request_filename !~ "\.(js|htc|ico|gif|jpg|png|css)$") {
                rewrite ^(.*) /app.php$1 last;
        }
    }


 location ~ \.php($|/) {
    set  $script     $uri;
    set  $path_info  "";

    if ($uri ~ "^(.+\.php)(/.+)") {
      set  $script     $1;
      set  $path_info  $2;
    }

    fastcgi_pass   127.0.0.1:9009;

    include fastcgi_params;
    fastcgi_buffers 8 16k;
    fastcgi_buffer_size 32k;
    fastcgi_param  SCRIPT_FILENAME  /home/username/my_webside/web$script;
    fastcgi_param  PATH_INFO        $path_info;
  }

}

#create symbolic link to enable a site
sudo ln -s /etc/nginx/sites-available/www.my_webside.lo /etc/nginx/sites-enabled/www.my_webside.lo

#restart nginx
sudo /etc/init.d/nginx restart
sudo /etc/init.d/php5-fpm restart
```