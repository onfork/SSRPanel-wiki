## 用chacha20加密方式需要安装libsodium
注意：libsodium从1.0.15开始就废弃了aes-128-ctr
```
yum install wget m2crypto git libsodium -y
yum -y groupinstall "Development Tools"
wget https://github.com/jedisct1/libsodium/releases/download/1.0.17/libsodium-1.0.17.tar.gz
tar xf libsodium-1.0.16.tar.gz && cd libsodium-1.0.16
./configure && make -j2 && make install
echo /usr/local/lib > /etc/ld.so.conf.d/usr_local_lib.conf
ldconfig
```