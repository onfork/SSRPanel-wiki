## 注册Linode
通过我的邀请链接注册账号并买VPS，有返利折扣的，注册链接如下：
https://www.linode.com/?r=2d4a0088743a2a06e3405514d486b8966c51a439

可以直接绑定信用卡支付，或者用银联绑定paypal，用paypal支付

## 创建VPS
注册 并登录 Linode，然后 找到 `Add a Linode`,
选择你需要购买的VPS配置，然后，Location 选择 `Fremont，CA` 或者 `Tokyo 2，JP` (这两个是优先推荐的)，其他任意（具体速度可以看看这个
https://www.linode.com/speedtest ，自己去一个个PING一遍，看看哪个适合你）
然后点`Add this Linode`则开始创建机器。

## 修改内核
创建新机器后，点Dashboard进去看主机详情，找到 Rebuild 点一下，选择centos7，然后网页滚倒最底部按钮点一下，它开始创建主机配置。
等他创建完之后再找到 profiles 点击进去选择 kernel 为 4.1.5-86_64-linode61 
然后boot（或者reboot）系统

## 安装基础命令工具
```
yum install -y wget vim unzip
```

## 安装锐速
```
安装：
wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh

卸载：
chattr -i /serverspeeder/etc/apx* && /serverspeeder/bin/serverSpeeder.sh uninstall -f
```

## 同步系统时间
```
timedatectl set-timezone Asia/Shanghai
```

## 安装shadowsocks
```
wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh
chmod +x shadowsocks.sh
./shadowsocks.sh 2>&1 | tee shadowsocks.log
```

## 修改最大文件链接数 NOFILE 设置
```
vim /etc/systemd/system.conf
DefaultLimitNOFILE=51200
```

## SS 自动重启监控
```
wget --no-check-certificate -O /opt/shadowsocks-crond.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-crond.sh
chmod 755 /opt/shadowsocks-crond.sh
(crontab -l ; echo "*/5 * * * * /opt/shadowsocks-crond.sh") | crontab -
crontab -l
service crond restart
```

## Firewalld 防火墙配置
打开 /etc/firewalld/zones/public.xml 文件，使用 <port protocol=”网路协议” port=”指定端口”/> 开放相应的端口：
```
<?xml version="1.0" encoding="utf-8"?>
<zone>
<short>Public</short>
<description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
<service name="dhcpv6-client"/>
<port protocol="tcp" port="指定端口"/>
<port protocol="tcp" port="开始端口-结束端口"/>
<port protocol="udp" port="开始端口-结束端口"/>
</zone>
```
重启 Firewalld 并查看端口配置是否生效
```
service firewalld restart
systemctl enable firewalld
firewall-cmd --zone=public --list-all
```
## 检查是否正常
检查锐速是否在运行
```
/serverspeeder/bin/serverSpeeder.sh status
```
检查 SS 是否在运行
```
/etc/init.d/shadowsocks status
```
检查 SS 运行是否正常（连接日志）
```
tail -f /var/log/shadowsocks.log
```
## 启动、停止、重启、状态
```
启动：/etc/init.d/shadowsocks start
停止：/etc/init.d/shadowsocks stop
重启：/etc/init.d/shadowsocks restart
状态：/etc/init.d/shadowsocks status
```

## 单/多用户配置
配置文件路径：/etc/shadowsocks.json
#### 单用户配置文件示例：
```
{
    "server":"0.0.0.0",
    "server_port":your_server_port,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"your_password",
    "timeout":300,
    "method":"your_encryption_method",
    "fast_open": false
}
```

#### 多用户多端口配置文件示例：
```
{
    "server":"0.0.0.0",
    "local_address":"127.0.0.1",
    "local_port":1080,
    "port_password":{
         "8989":"password0",
         "9001":"password1",
         "9002":"password2",
         "9003":"password3",
         "9004":"password4"             // 最后一行一定不能有,号
    },
    "timeout":300,
    "method":"your_encryption_method",
    "fast_open": false
}
```

## 卸载shadowsocks
```
./shadowsocks.sh uninstall
```