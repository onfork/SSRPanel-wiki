**SSR Panel 前端部署：**

首先你应该有 LNMP 的环境，简单粗暴。

	⁃	PHP 7.1
	⁃	MySQL 5.5+

打开 php.ini 搜索 disable_functions，把 proc_ 开头的函数都删掉并重启 PHP。

打开 phpMyAdmin，创建一个数据库用户和同名的数据库。并将 https://github.com/ssrpanel/ssrpanel/tree/master/sql 目录下的 db.sql 导入。

按正常方式新建一个站点，此处以 /data/wwwroot/www.domain.com 为例

```
yum -y install git

cd /data/wwwroot/www.domain.com

# 注意，此处会将代码 Clone 到当前目录，而不是新建一个 ssrpanel 的文件夹。
git clone https://github.com/ssrpanel/ssrpanel.git tmp && mv tmp/.git . && rm -rf tmp && git reset --hard

php composer.phar install

cp .env.example .env

php artisan key:generate

chown -R www:www storage/

chmod -R 777 storage/
```

修改站点的 Nginx 配置文件，将站点路径后加 /public 。例如：root  /data/wwwroot/www.domain.com/public

站点的 Nginx 配置文件加入以下内容配置伪静态：

```
location / {
    try_files $uri $uri/ /index.php$is_args$args;
}
```

打开 `nginx/conf/fastcgi.conf` 查找 `fastcgi_param PHP_ADMIN_VALUE "open_basedir=$document_root/:/tmp/:/proc/";`。
如果有就把它注释掉并重启 php-fpm，如果没有就不必更改。

重启 Nginx ( reload)。

打开站点目录下 config\database.php 在其中配置数据库信息。

在浏览器打开你的站点即部署成功。

账户：admin
密码：123456

**前端更新方法：**

```
# 在项目根目录 git pull，例如：

cd /data/wwwroot/www.domain.com

git pull
```

**SSR Panel 后端部署（CentOS）：**

先在前端新建一个节点，并记住它的 Node ID。

```
yum -y update

yum -y install git

yum -y groupinstall "Development Tools"

wget https://github.com/jedisct1/libsodium/releases/download/1.0.13/libsodium-1.0.13.tar.gz

tar xf libsodium-1.0.13.tar.gz && cd libsodium-1.0.13

./configure && make -j2 && make install

echo /usr/local/lib > /etc/ld.so.conf.d/usr_local_lib.conf

ldconfig

git clone -b manyuser https://github.com/shadowsocksrr/shadowsocksr.git

cd shadowsocksr

./setup_cymysql.sh

./initcfg.sh
```

打开 userapiconfig.py 将相关条目对修改成如下：
API_INTERFACE = 'glzjinmod'

打开 user-config.json 将 connect_verbose_info 的值设置为 1

打开 usermysql.json 写入你的数据库信息和 Node ID。
注：前后端同机器地址为 127.0.0.1 或 localhost，不同机器地址为前端IP，并确保前端数据库可远程连接并开放了 3306 端口。

运行：
 
在项目根目录执行

` python server.py`

这时可查看有运行情况，检查有没有错误。如果服务端没有错误，而连接不上，需要检查 iptables 或 firewall(CentOS 7) 的防火墙配置

####以下为通过脚本运行#### 以下命令在项目根目录下执行：

后台运行（无 log，ssh 窗口关闭后也继续运行）
` ./run.sh`

后台运行（输出 log，ssh 窗口关闭后也继续运行）
` ./logrun.sh`

后台运行时查看运行情况
` ./tail.sh`

停止运行
` ./stop.sh`

注：通过脚本运行默认日志会保存在根目录的 ssserver.log，可手动查看。

仅是基本的部署，需长期运行请使用 supervisord 来守护进程。

如有错误请指正。。