## 使用条件
```
连接设备的网卡上有2开头的Global类IPv6地址才能使用
```

## SSR(R)设置
将 `user-config.json` 中的  `"dns_ipv6"` 的 值由 `false` 改为 `true`

配置项保持默认值False时，节点不会向DNS请求IPv6结果，改完之后SSR(R)可接受IPv6连接。


另外，DNS设置成1.1.1.1那个了。
测试了下，节点到它的延迟低于1ms

```
多用户DNS：
echo -e "1.1.1.1 53
1.0.0.1 53
2606:4700:4700::1111 53
2606:4700:4700::1001 53" > /root/shadowsocksr/dns.conf

单用户DNS：
echo -e "1.1.1.1 53
1.0.0.1 53
2606:4700:4700::1111 53
2606:4700:4700::1001 53" > /root/shadowsocksr/shadowsocks/dns.conf
```