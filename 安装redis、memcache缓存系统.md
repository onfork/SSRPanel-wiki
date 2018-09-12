## 为什么用redis
SSRPanel是基于laravel开发的，laravel对redis的支持性非常的好，其默认的缓存系统是使用file即文件缓存，读取速度有时候较慢。
如果想加速网站的打开速度，可以使用redis，将原本放在磁盘上的file文件里的临时数据放到系统内存里，只需要更改SSRPanel/config/cache.php里的对应值即可
## 安装redis
```
wget http://download.redis.io/releases/redis-4.0.11.tar.gz
tar zxvf redis-4.0.11.tar.gz
cd redis-4.0.11
make && make install

复制配置
cp redis.conf /etc/redis.conf

编辑 /etc/redis.conf 中的daemon no 改为 daemon yes

运行redis
/usr/local/bin/redis-server /etc/redis.conf
```

## 安装memcache
```
wget http://memcached.org/latest
tar -zxvf memcached-1.x.x.tar.gz
cd memcached-1.x.x
./configure && make && make test && sudo make install
```