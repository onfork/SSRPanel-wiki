执行`sh logrun.sh`后发现无法正常启动，密码都带了一个b，端口无法正常启动

#### 现象
```
2019-05-08 09:16:23 INFO     server_pool.py:153 starting server at 0.0.0.0:7846
2019-05-08 09:16:23 WARNING  server_pool.py:165 IPV4 [Errno 98] Address already in use 
2019-05-08 09:16:23 INFO     db_transfer.py:211 db start server at port [5720] pass [b'KCtDB8'] protocol [b'origin'] method [b'aes-256-cfb'] obfs [b'plain']
2019-05-08 09:16:23 INFO     server_pool.py:127 starting server at [::]:5720
2019-05-08 09:16:23 INFO     server_pool.py:153 starting server at 0.0.0.0:5720
2019-05-08 09:16:23 WARNING  server_pool.py:165 IPV4 [Errno 98] Address already in use 
2019-05-08 09:16:23 INFO     db_transfer.py:211 db start server at port [5324] pass [b'Hq6Jzj'] protocol [b'origin'] method [b'aes-256-cfb'] obfs [b'plain']
2019-05-08 09:16:23 INFO     server_pool.py:127 starting server at [::]:5324
2019-05-08 09:16:23 INFO     server_pool.py:153 starting server at 0.0.0.0:5324
2019-05-08 09:16:23 WARNING  server_pool.py:165 IPV4 [Errno 98] Address already in use 
2019-05-08 09:16:23 INFO     db_transfer.py:211 db start server at port [6674] pass [b'dTqQ2t'] protocol [b'origin'] method [b'aes-256-cfb'] obfs [b'plain']
2019-05-08 09:16:23 INFO     server_pool.py:127 starting server at [::]:6674
2019-05-08 09:16:23 INFO     server_pool.py:153 starting server at 0.0.0.0:6674
2019-05-08 09:16:23 WARNING  server_pool.py:165 IPV4 [Errno 98] Address already in use 
2019-05-08 09:16:23 INFO     db_transfer.py:211 db start server at port [6971] pass [b'w4xyEz'] protocol [b'origin'] method [b'aes-256-cfb'] obfs [b'plain']
2019-05-08 09:16:23 INFO     server_pool.py:127 starting server at [::]:6971
2019-05-08 09:16:23 INFO     server_pool.py:153 starting server at 0.0.0.0:6971
2019-05-08 09:16:23 WARNING  server_pool.py:165 IPV4 [Errno 98] Address already in use
```

#### 原因
因为 Debian / Ubuntu 系统对新手太友好了，都自带了Python 2.7 和 Python 3.5 （CentOS都特么的是2.x），而Python 2 和 3 是完全两个不一样的世界，SSR(R)并没有同时兼容，在启动脚本中，如果系统中有3则优先选3没有就选2，所以就出现上面那种 pass 里带一个b的错误

#### 解决
```
改一下 logrun.sh 脚本，把 
python_ver=$(ls /usr/bin|grep -e "^python[23]\.[1-9]\+$"|tail -1) 

中的 3去掉，如下：

python_ver=$(ls /usr/bin|grep -e "^python[2]\.[1-9]\+$"|tail -1)
```