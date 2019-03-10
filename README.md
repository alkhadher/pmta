

##### CentOS 关闭ipv6
```
echo 'net.ipv6.conf.all.disable_ipv6=1' >> /etc/sysctl.conf
echo 'net.ipv6.conf.default.disable_ipv6=1' >> /etc/sysctl.conf
echo 'net.ipv6.conf.lo.disable_ipv6=1' >> /etc/sysctl.conf
sysctl -p /etc/sysctl.conf
reboot  这个方法不生效


sed -i "s/GRUB_CMDLINE_LINUX=\"console=tty/GRUB_CMDLINE_LINUX=\"ipv6.disable=1 console=tty/g" /etc/default/grub && cat /etc/default/grub && grub2-mkconfig -o /boot/grub2/grub.cfg && reboot

```

##### 关闭防火墙

```
firewall-cmd --state
systemctl stop firewalld.service
systemctl disable firewalld.service
```


##### 安装MailWizz
```
yum install -y wget screen
screen -S lnmp

wget http://soft.vpser.net/lnmp/lnmp1.5.tar.gz -cO lnmp1.5.tar.gz && tar zxf lnmp1.5.tar.gz && cd lnmp1.5 && ./install.sh lnmp
 
 
安装imap

cd /root/lnmp1.5/src
tar -jxvf php-*.*.tar.bz2
cd /root/lnmp1.5/src/php**/ext/imap

yum -y install epel-release
yum -y install libc-client-devel
ln -s /usr/lib64/libc-client.so /usr/lib/libc-client.so

/usr/local/php/bin/phpize
./configure --with-php-config=/usr/local/php/bin/php-config --with-kerberos --with-imap-ssl
make && make install

vim /usr/local/php/etc/php.ini
echo 'extension=imap.so' >> /usr/local/php/etc/php.ini

disable_functions 删除exec , proc_open函数
lnmp restart


lnmp vhost add  域名 
track 域名需要追加到nginx conf hostname ,勿忘记

上传程序文件,完整走一遍安装
通过PHPMyAdmin导入备份数据
登陆测试
```

##### 安装Mumara (该版本ionCube 暂不支持PHP7 )
```
安装LNMP 
安装ioncube
启用php exec
innodb_buffer_size 注意设置，以免MySQL崩溃
安装imap 模块
cd /root/lnmp1.5
./addons.sh 

lnmp vhost add  域名 
上传程序文件,完整走一遍安装

通过PHPMyAdmin导入备份数据
登陆测试
```

##### 安装PMTA
```
yum install -y wget unzip
wget https://s3-us-west-1.amazonaws.com/origin-static/pmta/PowerMTA-4.5r11.zip

unzip pmta.zip
rpm -Uvh PowerMTA*.rpm
\cp etc/pmta/license /etc/pmta/license
\cp usr/sbin/pmtad /usr/sbin/pmtad
\cp config /etc/pmta/config

mkdir -p /etc/pmta/dkim/
\cp pem/private.pem /etc/pmta/dkim/blingnova.blingnova.net.pem

service pmta start
service pmta restart
```

```
DNS Record 添加
DKIM TXT记录
_dmarc
```

```
stats面板默认端口号时8080，修改为888，pmtahttpd 负责stats面板，未找到重启该服务的方式。所以暂用重启机器 reboot
ip:888 访问管理页面
```

##### PMTA卸载
```
 rpm -e PowerMTA
```
