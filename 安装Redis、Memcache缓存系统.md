SSRPanel是基于Laravel框架开发的，Laravel对Redis的支持非常的好，其默认的缓存系统是使用file即文件缓存，读取速度有时候较慢（服务器硬盘如果是SSD还好，如果是HDD...）。
如果想加速网站的打开速度，可以使用Redis，将原本放在磁盘上的file文件里的临时数据放到系统内存里，只需要更改 `/config/cache.php` 里的对应值即可

## 安装Redis
```
wget http://download.redis.io/releases/redis-4.0.11.tar.gz
tar zxvf redis-4.0.11.tar.gz
cd redis-4.0.11
make && make install

复制配置
cp redis.conf /etc/redis-6379.conf

编辑 /etc/redis-6379.conf 中的daemon no 改为 daemon yes

运行redis
/usr/local/bin/redis-server /etc/redis-6379.conf
```

## 安装Memcache
```
wget http://memcached.org/files/memcached-1.5.10.tar.gz
tar -zxvf memcached-1.5.10.tar.gz
cd memcached-1.5.10
./configure && make && make test && sudo make install
```