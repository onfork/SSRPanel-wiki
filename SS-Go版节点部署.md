- 作者：[rc452860](https://github.com/rc452860)

## 安装
- 下载安装对应的版本，授权并安装，安装时会提示输入连接信息，完成后自动生成配置文件，位于同目录下，名为 `config.json`

```
wget https://github.com/rc452860/vnet/releases/download/v0.0.4/vnet_linux_amd64
chmod a+x vnet_linux_amd64
./vnet_linux_amd64

[root@node ~]# ./vnet_linux_amd64 
WARN 2019-01-20 12:09:40 config.go[66] LoadConfig: /root/config.json is not exist
INFO 2019-01-20 12:09:40 server.go[21] main: cpu core: 1
? what is your host address? 127.0.0.1
? what is your host address? 127.0.0.1
? what is your database port? (3306) 3306
? what is your database port? 3306
? what is your username? root
? what is your username? root
? what is your password? ****
? what is your database name? ssrpanel
? what is your database name? ssrpanel
? what is your node id? 1
? what is your node id? 1
? what is your want rate? (1) 1

```

## 配置文件
- 编辑配置文件 `vim /root/config.json`

```
{
    "mode": "db",
    "dbconfig": {
        "host": "127.0.0.1",
        "user": "root",
        "passwd": "root",
        "port": "3306",
        "database": "ssrpanel",
        "rate": 1,
        "NodeId": 1,
        "SyncTime": 3000000000
    },
    "shadowsocks_options": {
        "tcp_timeout": 0,
        "udp_timeout": 0
    }
}
```

## 运行
- 执行 `./vnet_linux_amd64`

```
INFO 2019-01-20 12:05:26 db.go[173] func1: start port [7380]
INFO 2019-01-20 12:05:26 shadowsocks.go[94] ConfigLimitHuman: server port: 7380 limit is: 20480000
INFO 2019-01-20 12:05:26 shadowsocks.go[110] ConfigTimeout: 0.0.0.0:7380 timeout:3s
INFO 2019-01-20 12:05:26 shadowsocks.go[163] startTCP: listening TCP on 0.0.0.0:7380
INFO 2019-01-20 12:05:26 shadowsocks.go[337] startUDP: listening UDP on 0.0.0.0:7380
INFO 2019-01-20 12:05:26 db.go[173] func1: start port [7168]
INFO 2019-01-20 12:05:26 shadowsocks.go[94] ConfigLimitHuman: server port: 7168 limit is: 20480000
INFO 2019-01-20 12:05:26 shadowsocks.go[110] ConfigTimeout: 0.0.0.0:7168 timeout:3s
INFO 2019-01-20 12:05:26 shadowsocks.go[163] startTCP: listening TCP on 0.0.0.0:7168
INFO 2019-01-20 12:05:26 shadowsocks.go[337] startUDP: listening UDP on 0.0.0.0:7168
INFO 2019-01-20 12:05:26 db.go[173] func1: start port [7227]
INFO 2019-01-20 12:05:26 shadowsocks.go[94] ConfigLimitHuman: server port: 7227 limit is: 20480000
INFO 2019-01-20 12:05:26 shadowsocks.go[110] ConfigTimeout: 0.0.0.0:7227 timeout:3s
INFO 2019-01-20 12:05:26 shadowsocks.go[163] startTCP: listening TCP on 0.0.0.0:7227
INFO 2019-01-20 12:05:26 shadowsocks.go[337] startUDP: listening UDP on 0.0.0.0:7227
```
