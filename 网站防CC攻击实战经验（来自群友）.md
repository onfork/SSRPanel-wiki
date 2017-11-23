## 来自群友的实际CC对抗经验

#### 输入下面命令后发现不少连接超过100,最高1万都有,去看了下nginx日志,都有2G大了,说明有人在进行攻击行为
````
netstat -nat|grep -i '80'|wc -l
````

#### 对连接的IP按连接数量进行排序，查看TCP连接状态
````
netstat -ntu | awk '{print $5}' | cut -d: -f1 | sort | uniq -c | sort -n
````

#### 用了张戈的防CC脚本并设置连接超过10就banned时间600000000000秒
````
https://zhangge.net/5066.html
https://github.com/jagerzhang/CCKiller
````

#### 胖虎的建议
````
如果面板搭建好要开放出来，建议做如下处理：
1.加CDN，例如：CLOUDFLARE
2.网站可以有两个、三个、四个，反正都是同一套面板，数据库单独一台VPS跑，当有人打你的网站的时候，一个网站挂了还可以有其他备份站，反正都是连同一个数据库，然后主站、备份站都不要部署SSR服务，节点机就当成节点机用，不建议将网站、数据库、SSR服务全部部署在同一台VPS上。
（单机单节点隐患：当被ban、被攻击时所有用户无法连接；CC攻击消耗流量也大，普通VPS也就1000G/月，分分钟搞死你，建议平时多囤节点机（512M内存+的KVM机器））
3.强烈不建议节点名称用域名，请直接使用IP地址（胖虎已经被墙了2个域名了）
````

#### 建议主站只打开相关端口
````
firewall-cmd --zone=public --add-port=80/tcp --permanent
firewall-cmd --zone=public --add-port=443/tcp --permanent
firewall-cmd --zone=public --add-port=8888/tcp --permanent
firewall-cmd --zone=public --add-port=3306/tcp --permanent
firewall-cmd --zone=public --add-port=22/tcp --permanent
firewall-cmd --permanent --zone=public --add-port=10000-20000/tcp
重新载入
firewall-cmd --reload
查看
firewall-cmd --zone= public --query-port=80/tcp
````
