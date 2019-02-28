## 安装
- CentOS： `yum -y install supervisor`
- Debien/Ubuntu适用：`apt-get install supervisor`

## 配置
修改主配置文件：`vim /etc/supervisord.conf`

最后一行增加如下文本，若已有请忽略
```
[include]
files = supervisord.d/*.conf #扩展名ini改为conf
```

## 创建自配置文件
举例命名为ssrpanel.conf（可自定义）：`vim /etc/supervisord.d/ssrpanel.conf`
粘贴如下
```
[program:ssrpanel] #项目名称，可自定义
command=php /www/wwwroot/ssrpanel/artisan queue:work database --queue=default --timeout=60 --sleep=5 --tries=3 #执行命令，根据情况自行更改网站目录
autostart=true #是否与supervisor一起启动
autorestart=true #意外退出是否自动重启
user=root #执行用户
startsecs=5 #自动重启间隔，单位秒
```

## 设为开机自启
- `systemctl enable supervisord.service`

## 系统常用命令：
`systemctl start supervisord.service` #开启服务
`systemctl stop supervisord.service` #关闭服务
`systemctl status supervisord.service` #查询服务状态
`systemctl reload supervisord.service` #重新加载supervisor.service配置文件
`ps -ef | grep supervisord` #查看进程

## supervisorctl 常用命令：
`supervisorctl start|stop program_name` #启动/停止服务，program_name为项目名
`supervisorctl status` #查看所有任务状态
`supervisorctl shutdown` #关闭所有任务