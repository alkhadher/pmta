

##### CentOS 关闭ipv6
```
vi /etc/sysctl.conf
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1
reboot
```

##### 安装MailWizz
```
安装LNMP 
lnmp vhost add  域名
```
##### 安装PMTA
```
rpm -Uvh PowerMTA*.rpm
\cp license /etc/pmta/license

\cp config /etc/pmta/config

mkdir -p /etc/pmta/dkim/
\cp pem/private.pem /etc/pmta/dkim/blingnova.blingnova.net.pem

```

```
DKIM TXT记录

```
