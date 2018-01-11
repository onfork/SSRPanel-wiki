## 说明
```
1.swap大小推荐是实际内存的2倍。
2.搬瓦工默认系统中的swap大小只有实际内存的1/4，有些用到swap的进程老是被自动杀死。
3.买KVM不要买OVZ，没有swap！具体看这：https://github.com/ssrpanel/SSRPanel/wiki/VPS%E6%8E%A8%E8%8D%90&%E8%B4%AD%E4%B9%B0%E7%BB%8F%E9%AA%8C
4.本质上是加swap文件并挂载，而不是加swap分区，不建议直接改swap分区
5.下面的所有命令记得用root权限操作
```

## 查看现有的swap
```
free -m
swapon -s
```

## 创建swap(大小：1G，自己改count的值)
```
[root@node ~]# dd if=/dev/zero of=/swapfile count=1024 bs=1M
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB) copied, 1.05997 s, 1.0 GB/s

[root@node ~]# ls / | grep swapfile
swapfile
```

## 看一下是否创建成功
```
[root@node ~]# chmod 600 /swapfile
[root@node ~]# ls -lh /swapfile
-rw-------. 1 root root 1.0G Jan 11 09:46 /swapfile
```

## 启用swap配置
```
[root@node ~]# mkswap /swapfile
mkswap: /swapfile: warning: don't erase bootbits sectors
        on whole disk. Use -f to force.
Setting up swapspace version 1, size = 1048572 KiB
no label, UUID=70c30e2d-d235-4d41-bebc-e6eac80f53b7
```

## 启用swap分区
```
[root@node ~]# swapon /swapfile
[root@node ~]# free -m
            total      used      free    shared    buffers    cached
Mem:          243        239          3          0          1        156
-/+ buffers/cache:        80        162
Swap:        1151          0      1151
```

## 加入开机启动
```
vim /etc/fstab
在文件最后加入这行
/swapfile              swap                    swap    defaults        0 0
```

## 重启
```
reboot
```

## 结果
```
[root@node ~]# swapon -s
Filename                Type        Size    Used    Priority
/dev/vda2                              partition    131064    0    -2
/swapfile                              file        1048568    0    -1
```

```
[root@node ~]# top
top - 10:01:23 up 12 min,  1 user,  load average: 0.15, 0.04, 0.01
Tasks:  72 total,  1 running,  71 sleeping,  0 stopped,  0 zombie
Cpu(s):  0.0%us,  0.3%sy,  0.0%ni, 99.0%id,  0.0%wa,  0.0%hi,  0.3%si,  0.3%st
Mem:    248924k total,  136040k used,  112884k free,    9496k buffers
Swap:  1179632k total,        0k used,  1179632k free,    43104k cached
```