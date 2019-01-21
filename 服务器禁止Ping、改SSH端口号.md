服务器禁止Ping、修改SSH端口主要是减少互联网上大量存在的僵尸网络、机器人自动扫描探活，进而进行攻击（例如暴力破解密码），可以一定程度防止一些自动化攻击和小骇客的骚扰。更多服务器运维防护知识，可以加内部交流群讨论交流学习。

## 禁止Ping
```
vi /etc/sysctl.conf

加入：net.ipv4.icmp_echo_ignore_all = 1

sysctl -p
```

## 改SSH端口
#### CentOS 6
```
vi /etc/ssh/sshd_config

找到 
PermitRootLogin yes
Port 22
把Port改成新的

service sshd restart
```

#### CentOS 7
```
默认系统可以通过以下命令快速修改 sshd_config中的 SSH 端口：

sed -i "s/#Port 22/Port 新端口/g" /etc/ssh/sshd_config

另外由于 SELinux 默认在 CentOS 7 中启用，所以更改 SSH 端口需要同时更新 SElinux 的端口 。

需要安装 policycoreutils 组件来让 semanage 更新 SSHD 端口。

yum -y install policycoreutils-python
semanage port -a -t ssh_port_t -p tcp 新端口
```

#### 修改系统密码
```
sudo passwd root
输入两边密码即可
```