## CentOS下编译安装vnstat
```
1.必须是KVM，网卡名称时eth0，OVZ请自行摸索（其实就是改网卡名）
2.通过守护进程自动更新网卡流量到本地数据库文件
```

## 一键安装脚本
```
wget -N --no-check-certificate https://raw.githubusercontent.com/ssrpanel/ssrpanel/master/server/deploy_vnstat.sh;chmod +x deploy_vnstat.sh;./deploy_vnstat.sh
```

## 示例
``` 每小时
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

``` 每天
[root@api ~]# vnstat -d

 eth0  /  daily

         day         rx      |     tx      |    total    |   avg. rate
     ------------------------+-------------+-------------+---------------
     10/09/2017    10.57 GiB |    9.69 GiB |   20.26 GiB |    2.01 Mbit/s
     10/10/2017     5.88 GiB |    4.97 GiB |   10.85 GiB |    1.08 Mbit/s
     10/11/2017     2.60 GiB |    2.53 GiB |    5.13 GiB |  509.98 kbit/s
     10/12/2017     2.19 GiB |    1.65 GiB |    3.85 GiB |  382.48 kbit/s
     10/13/2017     5.29 GiB |    4.13 GiB |    9.41 GiB |  935.73 kbit/s
     10/14/2017     7.47 GiB |    6.92 GiB |   14.39 GiB |    1.43 Mbit/s
     10/15/2017     9.97 GiB |    9.30 GiB |   19.27 GiB |    1.92 Mbit/s
     10/16/2017     7.25 GiB |    6.60 GiB |   13.85 GiB |    1.38 Mbit/s
     10/17/2017     9.31 GiB |    7.89 GiB |   17.20 GiB |    1.71 Mbit/s
     10/18/2017    13.61 GiB |   12.35 GiB |   25.96 GiB |    2.58 Mbit/s
     10/19/2017     7.19 GiB |    6.19 GiB |   13.38 GiB |    1.33 Mbit/s
     10/20/2017     7.09 GiB |    6.67 GiB |   13.76 GiB |    1.37 Mbit/s
     10/21/2017    11.38 GiB |   10.75 GiB |   22.12 GiB |    2.20 Mbit/s
     10/22/2017     5.49 GiB |    5.17 GiB |   10.66 GiB |    1.06 Mbit/s
     10/23/2017    16.09 GiB |   14.66 GiB |   30.75 GiB |    3.06 Mbit/s
     10/24/2017     6.70 GiB |    5.85 GiB |   12.55 GiB |    1.25 Mbit/s
     10/25/2017    10.94 GiB |    9.46 GiB |   20.40 GiB |    2.03 Mbit/s
     10/26/2017    12.78 GiB |   11.82 GiB |   24.59 GiB |    2.45 Mbit/s
     10/27/2017     5.45 GiB |    5.03 GiB |   10.48 GiB |    1.04 Mbit/s
     10/28/2017     5.30 GiB |    5.16 GiB |   10.46 GiB |    1.04 Mbit/s
     10/29/2017     3.73 GiB |    3.73 GiB |    7.45 GiB |  741.08 kbit/s
     10/30/2017    13.19 GiB |   11.34 GiB |   24.53 GiB |    2.44 Mbit/s
     10/31/2017     7.35 GiB |    6.10 GiB |   13.45 GiB |    1.34 Mbit/s
     11/01/2017    13.33 GiB |   11.62 GiB |   24.95 GiB |    2.48 Mbit/s
     11/02/2017    10.70 GiB |    9.95 GiB |   20.65 GiB |    2.05 Mbit/s
     11/03/2017    14.16 GiB |   11.75 GiB |   25.91 GiB |    2.58 Mbit/s
     11/04/2017     9.05 GiB |    8.70 GiB |   17.75 GiB |    1.76 Mbit/s
     11/05/2017    12.31 GiB |   11.67 GiB |   23.97 GiB |    2.38 Mbit/s
     11/06/2017    13.62 GiB |   12.35 GiB |   25.97 GiB |    2.58 Mbit/s
     11/07/2017     6.03 GiB |    5.79 GiB |   11.81 GiB |    2.74 Mbit/s
     ------------------------+-------------+-------------+---------------
     estimated     14.08 GiB |   13.52 GiB |   27.61 GiB |
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
cp vnstatd /usr/bin/vnstatd
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