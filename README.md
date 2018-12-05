

##### CentOS 关闭ipv6
```
vi /etc/sysctl.conf
net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1

sysctl -p /etc/sysctl.conf

reboot
```

##### 关闭防火墙

```
查看防火墙状态
firewall-cmd --state

停止firewall
systemctl stop firewalld.service

禁止firewall开机启动
systemctl disable firewalld.service
```


##### 安装MailWizz
```
安装LNMP 
lnmp vhost add  域名 
track 域名需要追加到ngxin conf hostname ,勿忘记

上传程序文件,完整走一遍安装
通过PHPMyAdmin导入备份数据
登陆测试
```

##### 安装Mumara (该版本ionCube 暂不支持PHP7 )
```
安装LNMP 
安装ioncube
lnmp vhost add  域名 
上传程序文件,完整走一遍安装

通过PHPMyAdmin导入备份数据
登陆测试
```

##### 安装PMTA
```
wget https://s3-us-west-1.amazonaws.com/origin-static/pmta/PowerMTA-4.5r11.zip

rpm -Uvh PowerMTA*.rpm
\cp etc/pmta/license /etc/pmta/license
\cp usr/sbin/pmtad /usr/sbin/pmtad
\cp config /etc/pmta/config

mkdir -p /etc/pmta/dkim/
\cp pem/private.pem /etc/pmta/dkim/blingnova.blingnova.net.pem

#权限问题，所以放置在了Vhost目录下
mkdir -p /home/wwwroot/wizz.blingnova.net/tmpmail 
mkdir -p /home/wwwroot/wizz.blingnova.net/badmail
chown -R www /home/wwwroot
chgrp -R www /home/wwwroot


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
