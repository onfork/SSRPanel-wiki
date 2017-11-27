某些同学在执行`php composer.phar install`时，出现错误
90%可能是漏装了PHP的fileinfo扩展了，用宝塔的请直接在宝塔里安装

## 下载并解压PHP源码包（内含fileinfo扩展源码）
```
wget http://us.php.net/get/php-7.1.11.tar.gz/from/this/mirror && mv mirror php-7.1.11.tar.gz
tar zxvf php-7.1.11.tar.gz && cd php-7.1.11/ext
```

## 找到本地装好的PHP的ext目录，把下好fileinfo源码复制进去
```
cp -r fileinfo/ /usr/local/php/include/php/ext/
```

## 编译（找到phpize，在fileinfo目录里执行一下）
```
cd /usr/local/php/include/php/ext/fileinfo
/usr/local/php/bin/phpize
```

## 编译2（配置一下）
```
./configure

此步骤可能会出现错误：configure: error: Cannot find php-config. Please use --with-php-config=PATH
出现这种情况就找到php-config，用下面这个：
./configure --with-php-config=/usr/local/php/bin/php-config
```

## 生成so包
```
make && make install
```

## 它会生成一个包到指定位置
```
Installing shared extensions:     /usr/local/php/lib/php/extensions/no-debug-non-zts-20160303/
```

## 编辑php.ini把包引用进去
```
extension=/usr/local/php/lib/php/extensions/no-debug-non-zts-20160303/fileinfo.so
```

## 重启php-fpm
```
service php-fpm restart
```