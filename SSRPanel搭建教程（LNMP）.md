## 安装
#### 环境要求
````
PHP 7.1.3+ （必须）
MYSQL 5.5+ （推荐5.6）
内存 1G+ (推荐2G)
磁盘空间 10G+
PHP必须开启zip、xml、curl、gd2、fileinfo、openssl、mbstring组件
安装完成后记得编辑.env中 APP_DEBUG 改为 false
````

#### 编辑php.ini
````
找到php.ini
vim /usr/local/php/etc/php.ini

搜索disable_function
删除proc_开头的所有函数
````

#### NGINX 加入URL重写规则
````
location / {
    try_files $uri $uri/ /index.php$is_args$args;
}
````

#### 拉取代码
````
cd /home/wwwroot/
git clone https://github.com/ssrpanel/ssrpanel.git ssrpanel
chown -R www:www ssrpanel
chmod -R a+x ssrpanel
````

#### 定时任务
````
crontab加入如下命令（请自行修改php、ssrpanel路径）：
* * * * * php /home/wwwroot/ssrpanel/artisan schedule:run >> /dev/null 2>&1

注意运行权限，必须跟ssrpanel项目权限一致，否则出现各种莫名其妙的错误
例如用lnmp的话默认权限用户组是 www:www，则添加定时任务是这样的：
crontab -e -u www
````

#### 数据库
上面都配置完了，就可以创建一个utf8mb4的数据库，面板从V4.7.3开始带有自动安装功能，无需再手动导入数据库，所以请直接访问网址即可

#### 邮件配置
###### 使用SMTP发信
````
编辑 .env 文件，修改 MAIL_ 开头的配置
````

###### 使用Mailgun发信
[点这里](https://github.com/ssrpanel/SSRPanel/wiki/%E4%BD%BF%E7%94%A8Mailgun%E5%8F%91%E9%80%81%E9%82%AE%E4%BB%B6)

###### 使用队列处理邮件
从V4.7.2开始邮件全部走队列处理，所以必须在面板根目录下执行一次 `sh queue.sh`，而且每次重启系统后都需要执行，否则发不出邮件

###### 发邮件失败处理
````
出现 Connection could not be established with host smtp.exmail.qq.com [Connection timed out #110] 这样的错误
因为smtp发邮件必须用到25,26,465,587这四个端口，故需要允许这四个端口通信
````

## 英文版
````
修改 .env 的 APP_LOCALE 值为 en
语言包位于 resources/lang 下，可自行更改
````

## 日志分析（仅支持单机单节点）
````
找到SSR服务端所在的ssserver.log文件
进入ssrpanel所在目录，建立一个软连接，并授权
cd /home/wwwroot/ssrpanel/storage/app
ln -S ssserver.log /root/shadowsocksr/ssserver.log
chown www:www ssserver.log
````

## IP库
```
本项目使用的是纯真IPv4库，文件位于 storage/qqwrt.dat ；
同时也使用IPIP的免费IPv4库，文件位于 storage/ipip.ipdb
原理：纯真查到的是非大陆的IP则会用IPIP再去查一遍具体国家，因为纯真带有运营商信息（来自IPIP的手动尴尬脸）
```

## HTTPS
```
将 .env 文件里的 REDIRECT_HTTPS 值改为true，则全站强制走https
```

## 后端部署
###### 手动部署

- 无上报IP版本（推荐）：
````
wget https://github.com/ssrpanel/shadowsocksr/archive/V3.2.2.tar.gz
tar zxvf V3.2.2.tar.gz
cd shadowsocksr
sh ./setup_cymysql2.sh
配置 usermysql.json 里的数据库链接，NODE_ID就是节点ID，对应面板后台里添加的节点的自增ID，所以请先把面板搭好，搭好后进后台添加节点
````

- 会上报在线IP版本（不推荐）：
```
https://github.com/ssrpanel/shadowsocksr
```

## 单端口多用户
````
编辑节点的 user-config.json 文件：
vim user-config.json

将 "additional_ports" : {}, 改为以下内容：
"additional_ports" : {
    "80": {
        "passwd": "统一认证密码", // 例如 SSRP4ne1，推荐不要出现除大小写字母数字以外的任何字符
        "method": "统一认证加密方式", // 例如 aes-128-ctr
        "protocol": "统一认证协议", // 可选值：orgin、verify_deflate、auth_sha1_v4、auth_aes128_md5、auth_aes128_sha1、auth_chain_a
        "protocol_param": "#", // #号前面带上数字，则可以限制在线每个用户的最多在线设备数，仅限 auth_chain_a 协议下有效，例如： 3# 表示限制最多3个设备在线
        "obfs": "tls1.2_ticket_auth", // 可选值：plain、http_simple、http_post、random_head、tls1.2_ticket_auth
        "obfs_param": ""
    },
    "443": {
        "passwd": "统一认证密码",
        "method": "统一认证加密方式",
        "protocol": "统一认证协议",
        "protocol_param": "#",
        "obfs": "tls1.2_ticket_auth",
        "obfs_param": ""
    }
},

保存，然后重启SSR(R)服务。
客户端设置：

远程端口：80
密码：password
加密方式：aes-128-ctr
协议：auth_aes128_md5
混淆插件：tls1.2_ticket_auth
协议参数：1026:@123 (SSR端口:SSR密码)

或

远程端口：443
密码：password
加密方式：aes-128-ctr
协议：auth_aes128_sha1
混淆插件：tls1.2_ticket_auth
协议参数：1026:SSRP4ne1 (SSR端口:SSR密码)

经实测，节点后端使用auth_sha1_v4_compatible，可以兼容auth_chain_a
注意：如果想强制所有账号都走80、443这样自定义的端口的话，记得把 user-config.json 中的 additional_ports_only 设置为 true
警告：经实测单端口下如果用锐速没有效果，很可能是VPS供应商限制了这两个端口
提示：配置单端口最好先看下这个WIKI，防止踩坑：https://github.com/ssrpanel/ssrpanel/wiki/%E5%8D%95%E7%AB%AF%E5%8F%A3%E5%A4%9A%E7%94%A8%E6%88%B7%E7%9A%84%E5%9D%91

````
## 代码更新
````
进入到SSRPanel目录下
1.手动更新： git pull
2.强制更新： sh ./update.sh 
````

## 校时
````
如果架构是“面板机-数据库机-多节点机”，请务必保持各个服务器之间的时间一致，否则会产生：节点的在线数不准确、最后使用时间异常、单端口多用户功能失效等。
推荐统一使用CST时间并安装校时服务：
vim /etc/sysconfig/clock 把值改为 Asia/Shanghai
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

重启一下服务器，然后：
yum install ntp
ntpdate cn.pool.ntp.org
````
#### 每日自动校时（crontab）
```
0 0 * * * /usr/sbin/ntpdate cn.pool.ntp.org 
```

## 二开规范
````
如果有小伙伴要基于本程序进行二次开发，自行定制，请谨记一下规则（欢迎提PR，我会免费拉你入内部群的）
1.数据库表字段请务必使用蟒蛇法，严禁使用驼峰法
2.写完代码最好格式化，该空格一定要空格，该注释一定要注释，便于他人阅读代码
3.本项目中ajax返回格式都是 {"status":"fail 或者 success", "data":[数据], "message":"文本消息提示语"}
````