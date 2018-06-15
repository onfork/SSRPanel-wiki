## 为什么要卸载
```
默认购买的阿里云VPS都自带一个aliyundun和一个aliyun-service，名字叫阿里云盾（安骑士）
实质上是用来监控VPS是否安全，自动扫描进程、查杀病毒用的，会识别SS(R)进程
云盾IP来自阿里云的漏洞扫描机，它会定期探测VPS是否存在已知漏洞
（比如你装了一个WORDPRESS，过一阵子它会提醒你有漏洞，得花钱一键修复酱紫）
```

## 卸载阿里云盾监控
```
wget http://update.aegis.aliyun.com/download/uninstall.sh
chmod +x uninstall.sh
./uninstall.sh
```

```
wget http://update.aegis.aliyun.com/download/quartz_uninstall.sh
chmod +x quartz_uninstall.sh
./quartz_uninstall.sh
```

## 删除残留
```
pkill aliyun-service
rm -fr /etc/init.d/agentwatch /usr/sbin/aliyun-service
rm -rf /usr/local/aegis*
```

## 屏蔽云盾 IP
```
iptables -I INPUT -s 140.205.201.0/28 -j DROP
iptables -I INPUT -s 140.205.201.16/29 -j DROP
iptables -I INPUT -s 140.205.201.32/28 -j DROP
iptables -I INPUT -s 140.205.225.192/29 -j DROP
iptables -I INPUT -s 140.205.225.200/30 -j DROP
iptables -I INPUT -s 140.205.225.184/29 -j DROP
iptables -I INPUT -s 140.205.225.183/32 -j DROP
iptables -I INPUT -s 140.205.225.206/32 -j DROP
iptables -I INPUT -s 140.205.225.205/32 -j DROP
iptables -I INPUT -s 140.205.225.195/32 -j DROP
iptables -I INPUT -s 140.205.225.204/32 -j DROP
```