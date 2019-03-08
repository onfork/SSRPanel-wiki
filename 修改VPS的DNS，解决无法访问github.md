## 修改dns
`vim /etc/resolv.conf`

```
nameserver 8.8.8.8
nameserver 1.1.1.1
```

## 重启网卡
`systemctl restart network`