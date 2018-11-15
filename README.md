##### 安装PMTA
```
rpm -Uvh PowerMTA.*.rpm
\cp license /etc/pmta/license

\cp config /etc/pmta/config

mkdir -p /etc/pmta/dkim/
\cp pem/private.pem /etc/pmta/dkim/blingnova.blingnova.net.pem

```

```
DKIM TXT记录

```
