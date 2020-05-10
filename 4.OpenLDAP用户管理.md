
#### 一、使用客户端工具“LdapAdmin”登录OpenLDAP管理界面
(下载地址：http://www.ldapadmin.org/download/ldapadmin.html) <br />

**1、新建链接，运行LdapAdmin程序依次选择“Start > Connect > New connection”,双击“New connection”，填写如下连接信息：**
![](/images/1/89/ldap1.jpg)

<br />
**2、OpenLDAP登录，选择新创建的连接，输入管理员密码（默认admin），选择yes，如下图：**
![](/images/1/89/ldap2.jpg)
![](/images/1/89/ldap3.jpg)
![](/images/1/89/ldap4.jpg)

<br />
**3、OpenLDAP管理界面如下：**
![](/images/1/89/ldap5.jpg)

<br />
#### 二、创建OpenLDAP用户组
**1、新建ou，选择“dc=speech,dc=local”右键点击“New > Organizational Unit”如下图：**
![](/images/1/89/ldap6.jpg)
![](/images/1/89/ldap7.jpg)

<br />
**2、在“ou=G01”下创建用户组“G01”，选择“ou=G01”右键点击“New > Group”如下图（注意组id可以按需修改）：**
![](/images/1/89/ldap8.jpg)
![](/images/1/89/ldap9.jpg)

<br />
#### 三、创建OpenLDAP用户
**1、在“ou=G01”下创建用户“user1”，选择“ou=G01”右键点击“New > User”如下图（注意用户id可以按需修改，勾选“Shadow Account”）：**
![](/images/1/89/ldap10.jpg)
![](/images/1/89/ldap11.jpg)
![](/images/1/89/ldap12.jpg)

<br />
**2、设置用户“user1”初始密码，选择“uid=user1”右键点击“Set Password”如下图：**
![](/images/1/89/ldap13.jpg)
![](/images/1/89/ldap14.jpg)

<br />
**3、修改用户“user1”的“shadowLastChange”属性为0，表示用户登录即修改密码，选择用户属性“shadowLastChange”右键“Edit value”如下图：**
![](/images/1/89/ldap15.jpg)
![](/images/1/89/ldap16.jpg)

<br />
#### 四、使用OpenLDAP用户登录系统
**1、使用OpenLDAP用户登录系统（登录服务器已正确部署OpenLDAP客户端）**
![](/images/1/89/ldap17.jpg)
![](/images/1/89/ldap18.jpg)
![](/images/1/89/ldap19.jpg)
![](/images/1/89/ldap20.jpg)

<br />
#### 附录1：用户的shadowAccount对象属性：
- **shadowLastChange**
    密码从1970年1月1日开始, 到最近一次修改, 一共间隔了多少天. 比如这里指定成16967就表示2016年6月15日. 也可以直接获取当天的日期,方法为:在系统里useradd一个用户,查看/etc/shadow中该用户的第三个值, 即是该值. 该值如果设置成0, 则表示下次登陆将强制修改密码, 用户修改密码成功以后, 该值将发生对应的变化;
- **shadowMin**
    密码从shadowLastChange指定的日期开始, 到多少天以后才能再次修改密码, 防止某些人天天没事就修改密码, 此值设置成0表示不限制;
- **shadowMax**
    密码从shadowLastChange指定的日期开始, 到多少天以后过期(即多少天后必须更改密码);
- **shadowInactive**
    密码过期以后还可以登陆多少天(每次登陆都会要求更改密码), 如果超过此值指定的天数, 下次登陆时会提示Your account has expired; please contact your system administrator;
- **shadowWarning**
    提前多少天开始警告用户密码将会过期;
- **shadowExpire**
    密码从1970年1月1日开始, 多少天以后将会过期;
- **shadowFlag**
    暂时无用.
