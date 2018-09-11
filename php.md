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

在安装其他扩展的时候发现 缺少安装扩展：gd，zip

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

##### 使用PhpSpreadsheet 写excel文件

编写composer配置文件

```
{
    "require":
    {
        "phpoffice/phpspreadsheet":"*"
    }
}
```

```
composer install
```

会生成vendor 目录并安装对应的库。

demo：

```
<?php
    date_default_timezone_set("Asia/Shanghai");
    require 'vendor/autoload.php';

    use PhpOffice\PhpSpreadsheet\Spreadsheet;
    use PhpOffice\PhpSpreadsheet\Writer\Xlsx;
    use PhpOffice\PhpSpreadsheet\Style\NumberFormat;
    use PhpOffice\PhpSpreadsheet\Cell\DataType;

    $spreadsheet = new Spreadsheet();
    $sheet = $spreadsheet->getActiveSheet();
    $sheet->setCellValue('A1', 'Hello 你好 !');

    $sheet->getStyle('B')->getNumberFormat()->setFormatCode(NumberFormat::FORMAT_TEXT);
    $sheet->getStyle('C')->getNumberFormat()->setFormatCode(NumberFormat::FORMAT_TEXT);
    $sheet->getStyle('D')->getNumberFormat()->setFormatCode(NumberFormat::FORMAT_TEXT);
    $sheet->setCellValue('B1', '13599999999');
    $sheet->setCellValue('C1', '6222222222222222');
    $sheet->setCellValueExplicit('D1', '372926791825121232', DataType::TYPE_STRING);

    $writer = new Xlsx($spreadsheet);
    $writer->save('hello world.xlsx');
?>
加载已有xls文件：
<?php
    date_default_timezone_set("Asia/Shanghai");
    require 'vendor/autoload.php';

    use PhpOffice\PhpSpreadsheet\Spreadsheet;
    use PhpOffice\PhpSpreadsheet\Writer\Xlsx;
    use PhpOffice\PhpSpreadsheet\Style\NumberFormat;
    use PhpOffice\PhpSpreadsheet\Cell\DataType;
    use PhpOffice\PhpSpreadsheet\IOFactory;

    $spreadsheet = IOFactory::load('temp.xlsx');

	$worksheet = $spreadsheet->getActiveSheet();

//	$worksheet->getCell('A1')->setValue('John');
	$worksheet->getCell('A2')->setValue('Smith');
	$worksheet->getCell('D2')->setValue('123456789654123');
	$worksheet->getCell('E2')->setValue('6222222784565154');
	//通过工厂模式来写内容
	$writer = IOFactory::createWriter($spreadsheet, 'Xls');
	$writer->save('twrite.xls');
    
    
?>
```



