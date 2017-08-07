```
vim /usr/local/nginx/conf/fastcgi.conf
找到 fastcgi_param PHP_ADMIN_VALUE "open_basedir=$document_root/:/tmp/:/proc/"; 这句
把它注释掉
```

保存 重启nginx 且 重启 php-fpm 