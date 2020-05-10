

**1、服务端域名必须为证书CN（Common Name）所填写域名，否则会出现如下错误**
```shell
Oct 21 22:40:04 localhost nslcd[9024]: [495cff] <passwd="user1"> failed to bind to LDAP server ldaps://ldap.speech.local/: Can't contact LDAP server: TLS: hostname does not match CN in peer certificate
Oct 21 22:40:04 localhost nslcd[9024]: [495cff] <passwd="user1"> no available LDAP server found: Can't contact LDAP server
```

**2、密码不符合最小长度，默认不小于8位**
```shell
Oct 21 22:53:52 localhost nslcd[9101]: [6dd9ac] <pwmod="user1"> ldap_passwd_s() without old password failed: Constraint violation: Password fails quality checking policy
Oct 21 22:53:52 localhost nslcd[9101]: [6dd9ac] <pwmod="user1"> ldap_passwd_s() with old password failed: Constraint violation: Password fails quality checking policy
```

**3、密码不能使用历史密码，默认为3个**
```shell
Oct 21 22:55:09 localhost nslcd[9101]: [a1821b] <pwmod="user1"> ldap_passwd_s() without old password failed: Constraint violation: Password is in history of old passwords
Oct 21 22:55:09 localhost nslcd[9101]: [a1821b] <pwmod="user1"> ldap_passwd_s() with old password failed: Constraint violation: Password is in history of old passwords
```

**4、无法连接到OpenLDAP服务端，请检查到OpenLDAP服务端连接是否正确**
```shell
Oct 22 07:57:27 localhost nslcd[19033]: [caa567] <passwd="user1"> failed to bind to LDAP server ldaps://ldap.speech.local/: Can't contact LDAP server: Transport endpoint is not connected
Oct 22 07:57:27 localhost nslcd[19033]: [caa567] <passwd="user1"> no available LDAP server found, sleeping 1 seconds
```

**5、证书错误，查看客户端和服务端证书是否由同一个ca签发**
```shell
Oct 22 08:02:38 localhost nslcd[19608]: [8b4567] <passwd="user1"> failed to bind to LDAP server ldaps://ldap.speech.local/: Can't contact LDAP server: error:14090086:SSL routines:ssl3_get_server_certificate:certificate verify failed (self signed certificate in c...
Oct 22 08:02:38 localhost nslcd[19608]: [8b4567] <passwd="user1"> no available LDAP server found, sleeping 1 seconds
```

**6、该用户不允许登录此服务器，查看用户host属性值**
```shell
Oct 29 23:17:06 test01 nslcd[8842]: [c5bb4f] <authz="user1"> pam_authz_search "(&(objectClass=posixAccount)(uid=user1)(|(host=ALL)(host=192.168.9.123)(host=test01)(host=test01.speech.local)))" found no matches
```

