- 作者：[rc452860](https://github.com/rc452860)

## 优点
- 作者乃阿里系技术大佬，持续维护开发
- 占用内存小，速度快
- 大量适配本面板，面板中的用户限速、开关节点UDP、节点与用户等级关联、自定义DNS、允许开关IPv6等等

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
        "user": "ssrpanel",
        "passwd": "ssrpanel",
        "port": "3306",
        "database": "ssrpanel",
        "rate": 1,
        "NodeId": 1,
        "SyncTime": 3000,
        "OnlineSyncTime": 60000
    },
    "shadowsocks_options": {
        "tcp_timeout": 0,
        "udp_timeout": 0
    }
}
```

## 运行
- 执行 `./vnet_linux_amd64` ，看到如下一堆端口启动，说明已经跑起来了

```
INFO 2019-01-22 08:58:36 db.go[256] DBServiceMonitor: start port [7589]
INFO 2019-01-22 08:58:36 db.go[256] DBServiceMonitor: start port [7935]
INFO 2019-01-22 08:58:36 db.go[256] DBServiceMonitor: start port [7235]
INFO 2019-01-22 08:58:36 db.go[256] DBServiceMonitor: start port [7262]
INFO 2019-01-22 08:58:36 db.go[256] DBServiceMonitor: start port [7026]
INFO 2019-01-22 08:58:36 db.go[256] DBServiceMonitor: start port [7131]
INFO 2019-01-22 08:58:36 db.go[256] DBServiceMonitor: start port [7996]
```
