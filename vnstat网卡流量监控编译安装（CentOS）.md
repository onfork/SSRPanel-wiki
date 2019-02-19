## CentOS下编译安装vnstat
1.必须是KVM，网卡名称时eth0，OVZ请自行摸索（其实就是改网卡名）
2.通过守护进程自动更新网卡流量到本地数据库文件

## 一键安装脚本（推荐）
wget -N --no-check-certificate https://raw.githubusercontent.com/ssrpanel/SSRPanel/master/scripts/vnstat.sh;chmod +x deploy_vnstat.sh;./deploy_vnstat.sh


## 示例
``` 每小时
[root@ONEVPS180713013725 shadowsocksr]# vnstat -h
 eth0                                                                     10:43 
  ^                                 t                                           
  |            t                   rt                                           
  |      t    rt                   rt              t                            
  |     rt  t rt                   rt    rt        t                   rt       
  |  rt rt rt rt rt                rt rt rt        t                 t rt       
  |  rt rt rt rt rt  t          rt rt rt rt        t                rt rt       
  |  rt rt rt rt rt rt  t       rt rt rt rt rt    rt                rt rt rt    
  |  rt rt rt rt rt rt rt rt    rt rt rt rt rt rt rt                rt rt rt    
  |  rt rt rt rt rt rt rt rt    rt rt rt rt rt rt rt                rt rt rt    
  |  rt rt rt rt rt rt rt rt rt rt rt rt rt rt rt rt    rt    rt rt rt rt rt    
 -+---------------------------------------------------------------------------> 
  |  11 12 13 14 15 16 17 18 19 20 21 22 23 00 01 02 03 04 05 06 07 08 09 10    
                                                                                
 h  rx (MiB)   tx (MiB)      h  rx (MiB)   tx (MiB)      h  rx (MiB)   tx (MiB) 
11   2,930.44   2,977.31    19     618.86     624.27    03     276.12     274.06
12   3,491.42   4,188.30    20   2,724.68   2,816.37    04     667.38     620.03
13   3,249.15   3,408.14    21   4,383.06   4,839.51    05     302.34     288.84
14   4,186.15   4,664.17    22   3,099.88   3,312.50    06     877.42     907.47
15   3,194.04   3,359.74    23   3,508.27   3,751.07    07     729.76     764.31
16   2,416.78   2,546.58    00   2,187.67   2,180.36    08   2,835.64   2,966.21
17   1,807.86   2,205.73    01   1,872.46   1,890.15    09   3,620.02   3,767.13
18   1,595.14   1,729.75    02   2,325.82   3,956.24    10   2,132.74   2,268.79
```

``` 每天
[root@ONEVPS180713013725 shadowsocksr]# vnstat -d

 eth0  /  daily

         day         rx      |     tx      |    total    |   avg. rate
     ------------------------+-------------+-------------+---------------
     07/16/2018    59.35 GiB |   61.74 GiB |  121.09 GiB |   12.04 Mbit/s
     07/17/2018    37.91 GiB |   40.12 GiB |   78.02 GiB |    7.76 Mbit/s
     07/18/2018    62.46 GiB |   65.40 GiB |  127.86 GiB |   12.71 Mbit/s
     07/19/2018    59.53 GiB |   64.02 GiB |  123.55 GiB |   12.28 Mbit/s
     07/20/2018    52.54 GiB |   55.93 GiB |  108.47 GiB |   10.78 Mbit/s
     07/21/2018    50.93 GiB |   53.61 GiB |  104.54 GiB |   10.39 Mbit/s
     07/22/2018    60.56 GiB |   64.62 GiB |  125.18 GiB |   12.45 Mbit/s
     07/23/2018    49.34 GiB |   53.19 GiB |  102.54 GiB |   10.19 Mbit/s
     07/24/2018    49.67 GiB |   52.96 GiB |  102.64 GiB |   10.20 Mbit/s
     07/25/2018    74.69 GiB |   77.69 GiB |  152.38 GiB |   15.15 Mbit/s
     07/26/2018    53.30 GiB |   55.29 GiB |  108.59 GiB |   10.80 Mbit/s
     07/27/2018    71.54 GiB |   79.03 GiB |  150.57 GiB |   14.97 Mbit/s
     07/28/2018    60.51 GiB |   65.14 GiB |  125.65 GiB |   12.49 Mbit/s
     07/29/2018    85.05 GiB |  102.21 GiB |  187.26 GiB |   18.62 Mbit/s
     07/30/2018    66.85 GiB |   69.58 GiB |  136.43 GiB |   13.56 Mbit/s
     07/31/2018    95.13 GiB |  116.25 GiB |  211.38 GiB |   21.02 Mbit/s
     08/01/2018    74.84 GiB |  100.42 GiB |  175.26 GiB |   17.42 Mbit/s
     08/02/2018    66.00 GiB |   77.29 GiB |  143.29 GiB |   14.25 Mbit/s
     08/03/2018    79.40 GiB |  126.57 GiB |  205.97 GiB |   20.48 Mbit/s
     08/04/2018    72.28 GiB |   75.10 GiB |  147.38 GiB |   14.65 Mbit/s
     08/05/2018    54.19 GiB |   56.14 GiB |  110.33 GiB |   10.97 Mbit/s
     08/06/2018    58.88 GiB |   61.58 GiB |  120.46 GiB |   11.98 Mbit/s
     08/07/2018    52.12 GiB |   54.90 GiB |  107.01 GiB |   10.64 Mbit/s
     08/08/2018    62.91 GiB |   65.94 GiB |  128.86 GiB |   12.81 Mbit/s
     08/09/2018    62.15 GiB |   64.81 GiB |  126.96 GiB |   12.62 Mbit/s
     08/10/2018    54.85 GiB |   58.40 GiB |  113.26 GiB |   11.26 Mbit/s
     08/11/2018    53.38 GiB |   55.75 GiB |  109.13 GiB |   10.85 Mbit/s
     08/12/2018    51.26 GiB |   53.06 GiB |  104.31 GiB |   10.37 Mbit/s
     08/13/2018    63.61 GiB |   67.49 GiB |  131.10 GiB |   13.03 Mbit/s
     08/14/2018    17.24 GiB |   19.19 GiB |   36.44 GiB |    8.17 Mbit/s
     ------------------------+-------------+-------------+---------------
     estimated     38.92 GiB |   43.32 GiB |   82.24 GiB |
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