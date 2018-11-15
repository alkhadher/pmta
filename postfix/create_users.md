### 添加User
```
domain=file-js-eu.xyz  #需要手动修改

password='rS7PydIBmIw%!nB&X'

mkdir -p  /var/mail/vhosts/$domain/info
echo info@$domain:{plain}$password >> /etc/dovecot/users
echo info@$domain $domain/info/ >> /etc/postfix/virtual_mailbox_map

mkdir -p  /var/mail/vhosts/$domain/bounce
echo bounce@$domain:{plain}$password >> /etc/dovecot/users
echo bounce@$domain $domain/bounce/ >> /etc/postfix/virtual_mailbox_map

mkdir -p  /var/mail/vhosts/$domain/fbl
echo fbl@$domain:{plain}$password >> /etc/dovecot/users
echo fbl@$domain $domain/fbl/ >> /etc/postfix/virtual_mailbox_map
	
mkdir -p  /var/mail/vhosts/$domain/abuse
echo abuse@$domain:{plain}$password >> /etc/dovecot/users
echo abuse@$domain $domain/abuse/ >> /etc/postfix/virtual_mailbox_map
	
mkdir -p  /var/mail/vhosts/$domain/postermaster
echo postermaster@$domain:{plain}$password >> /etc/dovecot/users
echo postermaster@$domain $domain/postermaster/ >> /etc/postfix/virtual_mailbox_map
	
chown -R vmail:vmail /var/mail/*
postmap /etc/postfix/virtual_mailbox_map

service postfix restart && service dovecot restart

```

### 添加转发
```
echo bounce@file-js-eu.xyz fbl@file-js-eu.xyz >> /etc/postfix/virtual
postmap /etc/postfix/virtual
```
