## 作者
- [aiyahacke](https://github.com/aiyahacke)
- [项目详情](https://github.com/aiyahacke/ssrpanel-v2ray)

## 添加节点
先在SSRPanel后台添加一个V2ray节点
（端口为9999，因为ssrpanel-v2ray里的config.json里的默认配置是9999）

## 安装JDK8
```
# ubuntu
sudo apt install openjdk-8-jdk
# centos
yum install java-1.8.0-openjdk java-1.8.0-openjdk-devel
```

## 安装控制台
```
cd /root/
wget https://github.com/aiyahacke/ssrpanel-v2ray/releases/download/0.0.3/ssrpanel-v2ray-0.0.3.zip
unzip ssrpanel-v2ray-0.0.3.zip -d ssrpanel-v2ray
chmod -R a+x ssrpanel-v2ray
```

## 配置SSRPanel后台

添加节点  
基础信息按实际情况填写  
扩展信息的服务类型选择V2ray  

基础选项:  
- 额外ID (alterId)  
- 端口 (VMess协议的端口)
  
高级选项(不懂就不要动下面几个选项):  
- 传输协议  
- 伪装类型  
- 伪装域名  
- WS/H2路径  
- TLS  

## 配置节点端

在 releases 页面下载编译版
修改 config.properties

几个重点配置项
- v2ray.system (操作系统，可选linux和windows，v0.0.3以上)
- v2ray.arch (操作系统位数，可选32和64，v0.0.3以上)
- ~~v2ray.grpc.port (tag为api的传入连接的端口)~~ (v0.0.3以上自动获取)
- v2ray.tag (VMess协议的tag)
- v2ray.alter-id (与面板额外ID一致)
- node.id (面板添加节点后得到的节点ID)
- node.traffic-rate (与面板流量比例一致)

数据库配置(远程连接SSRPanel的数据库)
- datasource.url (数据库的连接URL, 格式为 jdbc:mysql://地址:端口/数据库名称?serverTimezone=GMT%2B8)
- datasource.username (用户名)
- datasource.password (密码)
```

## 运行控制台
```
cd /root/ssrpanel-v2ray
java -jar ssrpanel-v2ray-0.0.3.jar
```

## 注意
 - V2Ray是很费内存的，同样300个用户和SS(R)相比，512M内存的KVM跑SS(R)服务稳定不炸进程，而V2Ray则会炸进程，所以V2Ray至少得1G内存才够。当然根据你的在线用户数量来，V2Ray节点的内存推荐是SS(R)节点内存的两倍。
 - [VPS推荐&购买经验](https://github.com/ssrpanel/SSRPanel/wiki/VPS%E6%8E%A8%E8%8D%90&%E8%B4%AD%E4%B9%B0%E7%BB%8F%E9%AA%8C)

## 问题
 - 如果启动后只有LOGO，没有任何信息，请检查是否执行了 chmod 对两个文件夹都进行了授权了
 - 如果提示配置错误，请检查是否有复制 ssrpanel-v2ray 下的 config.json 到 v2ray-linux-64 下；还有，必须进入到ssrpanel-v2ray目录下执行java -jar ssrpanel-v2ray-0.0.2.jar，不然一样会报配置错误
 - 如果客户端连不上，检查一下服务器的防火墙（SELINUX/IPTABLES/FIREWALLD）是否放行端口
 - 更高级的用法，其实我也不懂（o(╥﹏╥)o）
 - 实测CentOS 6不知道为搭建正常但是无法连接，很诡异；内部群友实测可用：CentOS 7、Debian 9、Ubuntu
## 相关
- [docker issue](https://github.com/ssrpanel/SSRPanel/issues/1050)
- [docker 教程](https://bfv.tw/index.php/2018/10/30/%E6%90%AD%E5%BB%BA-ssrpanel-v2ray-docker/)