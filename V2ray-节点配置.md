## JAVA版
- 作者 [aiyahacke](https://github.com/aiyahacke)

#### 配置SSRPanel
###### 添加节点
先在后台添加一个V2ray节点
（端口为9999，因为ssrpanel-v2ray里的config.json里的默认配置是9999）

#### 配置节点端
###### 安装JDK8
```
# ubuntu
sudo apt install openjdk-8-jdk
# centos
yum install java-1.8.0-openjdk java-1.8.0-openjdk-devel
```

###### 安装控制台
```
cd /root/
wget https://github.com/aiyahacke/ssrpanel-v2ray/releases/download/0.0.3/ssrpanel-v2ray-0.0.3.zip
unzip ssrpanel-v2ray-0.0.3.zip -d ssrpanel-v2ray
chmod -R a+x ssrpanel-v2ray
cd ssrpanel-v2ray
```


###### 修改 config.properties 文件
```
几个重点配置项
- v2ray.system (操作系统，可选值：linux、windows)
- v2ray.arch (操作系统位数，可选值：32、64)
- v2ray.tag (VMess协议的tag)
- v2ray.alter-id (与面板里设定的额外ID一致)
- v2ray.level (用户等级，暂无用)
- node.id (面板添加节点后得到的节点ID)
- node.traffic-rate (与面板里设定的流量比例一致)

数据库配置(远程连接SSRPanel的数据库)
- datasource.url (数据库的连接URL, 格式为 jdbc:mysql://地址:端口/数据库名称?serverTimezone=GMT%2B8)
- datasource.username (用户名)
- datasource.password (密码)
```

#### 运行控制台
```
java -jar ssrpanel-v2ray-0.0.3-jar-with-dependencies.jar
```

#### 效果
```
[root@node2 ssrpanel-v2ray]# java -jar ssrpanel-v2ray-0.0.3-jar-with-dependencies.jar
  __  __ _           _           _   _      _
 |  \/  (_)___  __ _| | ____ _  | \ | | ___| |_
 | |\/| | / __|/ _` | |/ / _` | |  \| |/ _ \ __|
 | |  | | \__ \ (_| |   < (_| | | |\  |  __/ |_
 |_|  |_|_|___/\__,_|_|\_\__,_| |_| \_|\___|\__|

2018/12/28 01:07:56 [INFO] cn.moegezi.v2ray.node.process.V2rayUpdate: 开始检测V2Ray更新  
2018/12/28 01:07:58 [INFO] cn.moegezi.v2ray.node.process.V2rayUpdate: 检测到新版本V2Ray: v4.9.0  
2018/12/28 01:07:58 [INFO] cn.moegezi.v2ray.node.process.V2rayUpdate: 开始下载: https://github.com/v2ray/v2ray-core/releases/download/v4.9.0/v2ray-linux-64.zip  
Downloading [==============================] 100%
2018/12/28 01:08:00 [INFO] cn.moegezi.v2ray.node.process.V2rayUpdate: 开始解压: v2ray-linux-64.zip  
2018/12/28 01:08:01 [INFO] cn.moegezi.v2ray.node.process.V2rayUpdate: V2Ray已更新至 v4.9.0  
V2Ray 4.9.0 (Po) 20181212
A unified platform for anti-censorship.
2018/12/28 01:08:02 [INFO] com.zaxxer.hikari.HikariDataSource: HikariPool-1 - Starting...  
2018/12/28 01:08:05 [INFO] com.zaxxer.hikari.HikariDataSource: HikariPool-1 - Start completed.  
2018/12/28 01:08:05 [INFO] cn.moegezi.v2ray.node.process.V2rayDao: 更新在线用户数: NUMBER 0  
2018/12/28 01:08:05 [INFO] cn.moegezi.v2ray.node.process.V2rayDao: 更新节点负载信息: LOAD 0.23 0.07 0.06  
2018/12/28 01:08:12 [INFO] cn.moegezi.v2ray.node.process.V2rayGrpc: 更新用户: ADD 420 REMOVE 0
```

#### 问题
 - 如果启动后只有LOGO，没有任何信息，请检查是否执行了 chmod 对两个文件夹都进行了授权了
 - 必须进入到ssrpanel-v2ray目录下执行java -jar ssrpanel-v2ray-0.0.3-jar-with-dependencies.jar，不然一样会报配置错误
 - 如果客户端连不上，检查一下服务器的防火墙（SELINUX/IPTABLES/FIREWALLD）是否放行端口
 - 更高级的用法，其实我也不懂，去问作者吧，作者也在内部群（o(╥﹏╥)o）
 - 实测CentOS 6不知道为搭建正常但是无法连接，很诡异；内部群友实测可用：CentOS 7、Debian 9、Ubuntu
 - 务必请先将服务器的时区改为CST

## GO版本
- 作者 [ColetteContreras](https://github.com/ColetteContreras)

#### 配置
###### 安装
```
curl -L -s https://raw.githubusercontent.com/ColetteContreras/v2ray-ssrpanel-plugin/master/install-release.sh | sudo bash
```

###### 卸载
```
curl -L -s https://raw.githubusercontent.com/ColetteContreras/v2ray-ssrpanel-plugin/master/uninstall.sh | sudo bash
```

###### 配置示例
```
{
  "log": {
    "loglevel": "debug"
  },
  "api": {
    "tag": "api",
    "services": [
      "HandlerService",
      "LoggerService",
      "StatsService"
    ]
  },
  "stats": {},
  "inbounds": [{
    "port": 10086,
    "protocol": "vmess",
    "tag": "proxy"
  },{
    "listen": "127.0.0.1",
    "port": 10085,
    "protocol": "dokodemo-door",
    "settings": {
      "address": "127.0.0.1"
    },
    "tag": "api"
  }],
  "outbounds": [{
    "protocol": "freedom"
  }],
  "routing": {
    "rules": [{
      "type": "field",
      "inboundTag": [ "api" ],
      "outboundTag": "api"
    }],
    "strategy": "rules"
  },
  "policy": {
    "levels": {
      "0": {
        "statsUserUplink": true,
        "statsUserDownlink": true
      }
    },
    "system": {
      "statsInboundUplink": true,
      "statsInboundDownlink": true
    }
  },

  "ssrpanel": {
    // Node id on your SSR Panel
    "nodeId": 1,
    // every N seconds
    "checkRate": 60,
    // user config
    "user": {
      // inbound tag, which inbound you would like add user to
      "inboundTag": "proxy",
      "level": 0,
      "alterId": 16,
      "security": "none"
    },
    // db connection
    "mysql": {
      "host": "127.0.0.1",
      "port": 3306,
      "user": "root",
      "password": "ssrpanel",
      "dbname": "ssrpanel"
    }
  }
}
```

## GO版一键包
- 作者：[阿拉凹凸曼](https://github.com/828768)
```
wget https://raw.githubusercontent.com/828768/Shell/master/deploy_node.sh
bash deploy_node.sh
```

## 注意
 - V2Ray是很费内存的，同样300个用户和SS(R)相比，512M内存的KVM跑SS(R)服务稳定不炸进程，而V2Ray则会炸进程，所以V2Ray至少得1G内存才够。当然根据你的在线用户数量来，V2Ray节点的内存推荐是SS(R)节点内存的两倍。
 - [VPS推荐&购买经验](https://github.com/ssrpanel/SSRPanel/wiki/VPS%E6%8E%A8%E8%8D%90&%E8%B4%AD%E4%B9%B0%E7%BB%8F%E9%AA%8C)

## 相关
- [docker issue](https://github.com/ssrpanel/SSRPanel/issues/1050)
- [docker 教程](https://bfv.tw/index.php/2018/10/30/%E6%90%AD%E5%BB%BA-ssrpanel-v2ray-docker/)
- [JAVA install doc](https://github.com/aiyahacke/ssrpanel-v2ray)
- [Go install doc](https://github.com/ssrpanel/SSRPanel/issues/1222)
- [Go v2ray-ssrpanel-plugin](https://github.com/ColetteContreras/v2ray-ssrpanel-plugin)