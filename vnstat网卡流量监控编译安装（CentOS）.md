## CentOS下编译安装vnstat
```
1.必须是KVM，网卡名称时eth0，OVZ请自行摸索
2.通过守护进程自动更新网卡流量到本地数据库文件
```

## 示例
```
[root@ss ~]# vnstat -h
 eth0                                                                     16:03 
  ^                                                      t                      
  |                                                     rt                      
  |                                                  r  rt                      
  |                                                  rt rt                      
  |                                                  rt rt                      
  |                                                  rt rt                      
  |                                                  rt rt                      
  |                                      rt r        rt rt rt                   
  |     rt                      rt rt rt rt rt       rt rt rt                   
  |     rt                   rt rt rt rt rt rt       rt rt rt                   
 -+---------------------------------------------------------------------------> 
  |  17 18 19 20 21 22 23 00 01 02 03 04 05 06 07 08 09 10 11 12 13 14 15 16    
                                                                                
 h  rx (MiB)   tx (MiB)      h  rx (MiB)   tx (MiB)      h  rx (MiB)   tx (MiB) 
17     153.35     136.46    01     243.95     234.19    09   1,368.02   1,265.98
18     453.93     445.85    02     346.34     332.74    10   1,657.47   1,661.87
19      44.34      19.22    03     350.47     341.43    11     637.92     594.06
20     115.31      93.10    04     446.72     435.57    12      41.29      18.56
21      70.34      49.01    05     641.70     588.79    13      40.46      15.90
22     130.93      94.31    06     553.38     451.28    14      42.09      19.04
23      31.44       7.61    07     134.18     103.11    15      86.30      67.08
00      77.30      58.36    08     134.37      86.99    16       1.42       0.06
```

#### 下载解压
```
wget http://humdi.net/vnstat/vnstat-1.17.tar.gz
tar zxvf vnstat-1.17.tar.gz
cd vnstat-1.17
```

#### 编译安装
```
./configure
make && make install
```

#### 各种配置
```
mkdir /var/lib/vnstat
cp vnstat.conf.new /etc/vnstat.conf
vnstat --create -i eth0
vnstat -u -i eth0
```

#### 守护进程
```
cp vnstatd /usr/sbin/vnstatd
cp examples/init.d/centos/vnstat /etc/init.d/
chmod +x /etc/init.d/vnstat
chkconfig --add vnstat
chkconfig vnstat on
service vnstat start
```

#### 常用命令
```
vnstat -u
vnstat -h
vnstat -l
vnstat -u -i eth0
```