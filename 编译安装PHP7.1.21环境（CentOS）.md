## 0.安装一大堆必备的东西
先执行
```
yum install -y epel-release
yum install -y libmcrypt-devel
```

再执行
```
yum -y install gcc g++ gcc+ gcc-c++
yum -y install autoconf vim pv rsync
yum -y install pcre-devel openssl openssl-devel
yum -y install libxml2 libxml2-devel libmcrypt libXpm-devel libc-client-devel libcurl-devel libjpeg-devel libpng-devel libicu-devel openldap-devel
yum -y install curl gd2 gd unzip
yum -y install libevent-devel libxslt-devel freetype-devel unixODBC-devel aspell-devel readline-devel net-snmp-devel enchant-devel
yum -y install bzip2 bzip2-devel
yum -y install gmp-devel readline-devel net-snmp-devel libxslt-devel
```

#### 1.下载并解压PHP
````
wget http://php.net/get/php-7.1.21.tar.gz/from/this/mirror
mv mirror php-7.1.21.tar.gz
tar zxvf php-7.1.21.tar.gz
cd php-7.1.21
````

#### 2.配置PHP
```
./configure \
--prefix=/usr/local/php7 \
--enable-fpm \
--with-fpm-user=apache  \
--with-fpm-group=apache \
--enable-inline-optimization \
--disable-debug \
--disable-rpath \
--enable-shared  \
--enable-soap \
--with-libxml-dir \
--with-xmlrpc \
--with-openssl \
--with-mcrypt \
--with-mhash \
--enable-pcntl \
--with-pcre-regex \
--with-sqlite3 \
--with-zlib \
--enable-bcmath \
--with-iconv \
--with-bz2 \
--enable-calendar \
--with-curl \
--with-cdb \
--enable-dom \
--enable-exif \
--enable-fileinfo \
--enable-filter \
--with-pcre-dir \
--enable-ftp \
--with-gd \
--with-openssl-dir \
--with-jpeg-dir \
--with-png-dir \
--with-zlib-dir  \
--with-freetype-dir \
--enable-gd-native-ttf \
--enable-gd-jis-conv \
--with-gettext \
--with-gmp \
--with-mhash \
--enable-json \
--enable-mbstring \
--enable-mbregex \
--enable-mbregex-backtrack \
--with-libmbfl \
--with-onig \
--enable-pdo \
--with-mysqli=mysqlnd \
--with-pdo-mysql=mysqlnd \
--with-zlib-dir \
--with-pdo-sqlite \
--with-readline \
--enable-session \
--enable-shmop \
--enable-simplexml \
--enable-sockets  \
--enable-sysvmsg \
--enable-sysvsem \
--enable-sysvshm \
--enable-wddx \
--with-libxml-dir \
--enable-xml \
--with-xsl \
--enable-zip \
--with-snmp \
--enable-mysqlnd-compression-support \
--with-pear \
--enable-opcache
```

#### 3.编译
```
make && make install
```

#### 4.出错
```
configure: error: mcrypt.h not found. Please reinstall libmcrypt.
代码如下:

wget ftp://mcrypt.hellug.gr/pub/crypto/mcrypt/libmcrypt/libmcrypt-2.5.7.tar.gz
tar zxf libmcrypt-2.5.7.tar.gz
cd libmcrypt-2.5.7
./configure
make && make install

再重新执行第2步，然后再执行第3步
```

```
出现如下错误：
/root/php-7.1.21/ext/xmlrpc/libxmlrpc/encodings.c:74: undefined reference to `libiconv_open'

vim Makefile
找到 EXTRA_LIBS =
在最后添加 -liconv
保存
再 make && make install
```

#### 5.编辑php-fpm配置（用于启动PHP）
```
创建www用户组
groupadd www

把添加www用户并加入www组并禁止登录
useradd -g www www -s /sbin/nologin

生成php7的php-fpm
touch /usr/local/php7/etc/php-fpm.conf
vim /usr/local/php7/etc/php-fpm.conf

将下面内容黏贴进去并保存：
[global]
pid = /usr/local/php7/var/run/php-fpm.pid
error_log = /usr/local/php7/var/log/php-fpm.log
log_level = notice

[www]
listen = /tmp/php7-cgi.sock
listen.backlog = -1
listen.allowed_clients = 127.0.0.1
listen.owner = www
listen.group = www
listen.mode = 0666
user = www
group = www
pm = dynamic
pm.max_children = 50
pm.start_servers = 5
pm.min_spare_servers = 5
pm.max_spare_servers = 50
request_terminate_timeout = 100
request_slowlog_timeout = 0
slowlog = var/log/slow.log
```

#### 6.修改NGINX配置，让NGINX用PHP来解析PHP
```
vim /usr/local/nginx/conf/vhost/xxx.com.conf
找到 fastcgi_pass 
将 unix:/tmp/php-cgi.sock; 改为  unix:/tmp/php7-cgi.sock; 
```

### 
```
把php.ini 拷贝到 /usr/local/php7/lib/下
```

#### 7.启动php-fpm
```
/usr/local/php7/sbin/php-fpm
```

#### 8.重启NGINX
```
/usr/local/nginx/sbin/nginx -s reload
```

#### 9.快捷命令
```
执行如下命令，即可直接在ssh里执行php命令
ln -s /usr/local/php7/bin/php /usr/sbin/php
```
