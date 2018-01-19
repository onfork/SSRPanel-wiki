VPS到手之后，有些内核锐速是不支持的，所以需要换一下
## CentOS 6
#### 使用epel（推荐）
```
yum install epel-release -y
yum update -y
yum install kernel-2.6.32-573.1.1.el6.x86_64 -y
```

#### 使用91yun提供的内核
```
rpm -ivh http://soft.91yun.org/ISO/Linux/CentOS/kernel/kernel-firmware-2.6.32-504.3.3.el6.noarch.rpm --force
rpm -ivh http://soft.91yun.org/ISO/Linux/CentOS/kernel/kernel-2.6.32-504.3.3.el6.x86_64.rpm --force
```

## CentOS 7
```
rpm -ivh http://soft.91yun.org/ISO/Linux/CentOS/kernel/kernel-3.10.0-229.1.2.el7.x86_64.rpm --force
```

完了reboot重启下VPS