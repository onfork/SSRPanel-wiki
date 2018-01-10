## 先装zlib
```
sudo yum install -y zlib zlib-devel
```

## 安装setuptools
```
wget https://pypi.python.org/packages/source/s/setuptools/setuptools-0.6c11.tar.gz
tar zxvf setuptools-0.6c11.tar.gz && cd setuptools-0.6c11
sudo python setup.py build
sudo python setup.py install
```

## 安装meld
```
wget https://pypi.python.org/packages/45/a0/317c6422b26c12fe0161e936fc35f36552069ba8e6f7ecbd99bbffe32a5f/meld3-1.0.2.tar.gz#md5=3ccc78cd79cffd63a751ad7684c02c91
tar zxvf meld3-1.0.2.tar.gz && cd meld3-1.0.2
python setup.py install
ldconfig
```

## 下载源码
```
wget https://pypi.python.org/packages/31/7e/788fc6566211e77c395ea272058eb71299c65cc5e55b6214d479c6c2ec9a/supervisor-3.3.3.tar.gz
tar zxvf supervisor-3.3.3.tar.gz && cd supervisor-3.3.3
```

## 安装
```
python setup.py install
```

## 生成配置文件
```
echo_supervisord_conf > /etc/supervisord.conf
```

## 加入配置（要守护的进程）
```
vim /etc/supervisord.conf
```

复制以下内容到 文件末尾
```
[program:shadowsocksr]
directory=/root/shadowsocksr
command=python server.py m
user=root
autostart = true
autoresart = true
stderr_logfile = /root/shadowsocksr/ssserver.log
stdout_logfile = /root/shadowsocksr/ssserver.log
stderr_logfile_maxbytes=10MB
stderr_logfile_backups=10
startsecs=3
```

## 加载配置
```
supervisord
supervisorctl reread
supervisorctl reload
```

## 查看是否守护中
```
[root@node shadowsocksr]# supervisorctl status
shadowsocksr                    RUNNING  pid 30993, uptime 0:08:13

[root@node shadowsocksr]# ps aux |grep python
root    30399  0.0  3.1  16076  7792 ?        Ss  13:46  0:01 /usr/bin/python2.6 /usr/bin/supervisord
root    30993  0.4  4.5  40808 11216 ?        Sl  14:47  0:02 python server.py m
root    31048  0.0  0.3  4420  776 pts/1    S+  14:55  0:00 grep python
```