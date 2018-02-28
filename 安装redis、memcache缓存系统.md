## 安装redis
```
wget http://download.redis.io/releases/redis-4.0.8.tar.gz
tar zxvf redis-4.0.8.tar.gz
cd redis-4.0.8
make && make install

复制配置
cp redis.conf /etc/redis.conf

编辑 /etc/redis.conf 中的daemon no 改为 daemon yes

运行redis
/usr/local/bin/redis-server /etc/redis.conf
```

## 安装memcache
```

```