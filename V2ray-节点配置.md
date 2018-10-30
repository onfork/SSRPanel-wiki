## 作者
[aiyahacke](https://github.com/aiyahacke)

## 先在SSRPanel后台添加一个V2ray节点（端口为10087，因为ssrpanel-v2ray里的config.json里的默认配置是10087）
## 安装控制台
```
cd /root/
wget https://github.com/aiyahacke/ssrpanel-v2ray/releases/download/0.0.2/ssrpanel-v2ray-0.0.2.zip
unzip ssrpanel-v2ray-0.0.2.zip -d ssrpanel-v2ray
chmod -R a+x ssrpanel-v2ray
```

## 下载v2ray core
```
cd /root/
wget wget https://github.com/v2ray/v2ray-core/releases/download/v3.49/v2ray-linux-64.zip
unzip v2ray-linux-64.zip -d v2ray-linux-64
chmod -R a+x v2ray-linux-64
```

## 复制配置文件至v2ray core
```
cp /root/ssrpanel-v2ray/config.json /root/v2ray-linux-64/
```

## 修改控制台配置
```
cd ssrpanel-v2ray
vim config.properties

几个重点配置项
  v2ray.path=/root/v2ray-linux-64 （就是上面那个v2ray core的地址）
  v2ray.grpc.port (tag为api的传入连接的端口)
  v2ray.tag (VMess协议的tag)
  v2ray.alter-id (与面板里设置的额外ID一致)
  node.id (面板添加节点后得到的节点ID)
  node.traffic-rate (与面板流量比例一致)

数据库配置(远程连接SSRPanel的数据库)
  datasource.url (数据库的连接URL, 格式为 jdbc:mysql://地址:端口/数据库名称?serverTimezone=GMT%2B8)
  datasource.username (用户名)
  datasource.password (密码)
```

## 运行控制台
```
java -jar /root/ssrpanel-v2ray/ssrpanel-v2ray-0.0.2-SNAPSHOT.jar
```

## 问题
 - 如果启动后只有LOGO，没有任何信息，请检查是否执行了 chmod 对两个文件夹都进行了授权了
 - 如果提示配置错误，请检查是否有复制 ssrpanel-v2ray 下的 config.json 到 v2ray-linux-64 下
 - 如果客户端连不上，检查一下服务器的防火墙（SELINUX/IPTABLES/FIREWALLD）是否放行端口
 - 更高级的用法，其实我也不懂（o(╥﹏╥)o）
 - 实测CentOS 6不知道为搭建正常但是无法连接，很诡异；内部群友实测可用：CentOS 7、Debian 9、Ubuntu
## 相关
- [docker issue](https://github.com/ssrpanel/SSRPanel/issues/1050)
- [docker 教程](https://bfv.tw/index.php/2018/10/30/%E6%90%AD%E5%BB%BA-ssrpanel-v2ray-docker/)