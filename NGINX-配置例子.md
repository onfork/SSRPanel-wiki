NGINX 配置例子
推荐使用LNMP傻瓜化添加虚拟机
lnmp vhsot add
```
server
{
	listen 80;
	server_name www.xxx.com;
	index index.html index.htm index.php default.html default.htm default.php;
	root  /home/wwwroot/ssrpanel/public; # 注意这里，是指向ssrpanel的public目录

	include other.conf;
	location ~ [^/]\.php(/|$)
	{
		try_files $uri =404;
		fastcgi_pass  unix:/tmp/php7-cgi.sock;
		fastcgi_index index.php;
		include fastcgi.conf;
		#include pathinfo.conf;
	}

	location ~ .*\.(gif|jpg|jpeg|png|bmp|swf)$
	{
		expires      30d;
	}

	location ~ .*\.(js|css)?$
	{
		expires      12h;
	}

        # 注意这里，必须加入以下url重写规则
	location / {
		try_files $uri $uri/ /index.php$is_args$args;
	}

	access_log  /home/wwwlogs/www.xxx.com_access.log;
	error_log  /home/wwwlogs/www.xxx.com_error.log;
}
```