## 禁止PING
```
vi /etc/sysctl.conf

加入：net.ipv4.icmp_echo_ignore_all = 1

sysctl -p
```

## 改端口
```
vi /etc/ssh/sshd_config

找到 
PermitRootLogin yes
Port 22
把Port改成新的

service sshd restart
```