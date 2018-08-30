## 禁止PING
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

## CentOS 7
```
默认系统可以通过以下命令快速修改 sshd_config中的 SSH 端口：

sed -i "s/#Port 22/Port 新端口/g" /etc/ssh/sshd_config

另外由于 SELinux 默认在 CentOS 7 中启用，所以更改 SSH 端口需要同时更新 SElinux 的端口 。

需要安装 policycoreutils 组件来让 semanage 更新 SSHD 端口。

yum -y install policycoreutils-python
semanage port -a -t ssh_port_t -p tcp 新端口
```