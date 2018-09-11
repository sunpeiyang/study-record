# php 笔记

## php 安装使用

下载 php-5.6.30.tar.gz， 编译安装

```
tar -xzxv php-5.6.30.tar.gz
./configure --prefix=/usr/local/php --with-config-file-path=/etc/ --with-mysql --with-zlib-dir=/usr/local/zlib/
 --enable-soap --enable-mbstring=all --enable-sockets --enable-fpm --with-openssl
make
make install

cp php.ini-development /usr/local/php/etc/php.ini
cp /usr/local/php/etc/php-fpm.conf.default /usr/local/etc/php-fpm.conf
cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf

cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
```

启动php

```
service start php-fpm
```

php --ini 查看php加载的配置文件。

##### redis 扩展：

```
下载扩展包https://github.com/phpredis/phpredis
cd phpredis
phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make install
```

##### pgsql 扩展：

```
在php编译环境下
cd ext/pgsql/
/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config
make && make instal
```

配置php.ini 文件：

extension\_dir = "/usr/local/php/lib/php/extensions/no-debug-non-zts-20151012"

extension=pgsql.so

extension=redis.so

php -m 查看加载了哪些扩展。

##### composer 安装

```
curl -sS https://getcomposer.org/installer | php
或者
php -r "readfile('https://getcomposer.org/installer');" | php
mv composer.phar /usr/local/bin/composer
```



