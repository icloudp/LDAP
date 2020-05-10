
#### 一、OpenLDAP数据备份
```shell
# ldapctl cat > openldap_backup_20191023.ldif
```

<br />
#### 二、OpenLDAP数据恢复
**1、安装OpenLDAP服务端，删除默认mdb文件**
```shall
# cd /usr/local/openldap/var/openldap-data
# rm -fr *.mdb
```

**2、重启openldap服务**
```shell
# ldapctl restart
Stopping OpenLDAP (pid: 8657)   [ OK ]
Starting OpenLDAP (pid: 8695)   [ OK ]
```

**3、恢复备份数据**
```shell
# /usr/local/openldap/sbin/slapadd -v -l openldap_backup_20191023.ldif 
added: "dc=speech,dc=local" (00000001)
added: "ou=ppolicy,dc=speech,dc=local" (00000002)
added: "cn=defaults,ou=ppolicy,dc=speech,dc=local" (00000003)
added: "ou=sudoers,dc=speech,dc=local" (00000004)
added: "cn=defaults,ou=sudoers,dc=speech,dc=local" (00000005)
added: "ou=G01,dc=speech,dc=local" (00000006)
added: "cn=G01,ou=G01,dc=speech,dc=local" (00000007)
added: "uid=user1,ou=G01,dc=speech,dc=local" (00000008)
_#################### 100.00% eta   none elapsed            none fast!         
Closing DB...
```
