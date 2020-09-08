#### 安装 JDK

```
~]# yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel
~]# java -version
openjdk version "1.8.0_262"
OpenJDK Runtime Environment (build 1.8.0_262-b10)
OpenJDK 64-Bit Server VM (build 25.262-b10, mixed mode)

```

#### 安装数据库

1.  Adding the MySQL Yum Repository

```
~]# wget https://dev.mysql.com/get/mysql80-community-release-el7-2.noarch.rpm
~]# rpm -ivh mysql80-community-release-el7-2.noarch.rpm
```

2.  Selecting a Release Series

```
~]# yum repolist all | grep mysql
~]# yum install yum-utils
~]# yum-config-manager --disable mysql80-community
~]# yum-config-manager --enable mysql57-community
```

3. Installing MySQL

```
~]# yum install -y mysql-community-server
```

4. Configure MySQL

```
[mysqld]
skip_name_resolve=on
innodb_file_per_table=on
collation_server=utf8_unicode_ci
character_set_server=utf8
skip-character-set-client-handshake
innodb_log_file_size=2GB
max_allowed_packet=256m
sql_mode=ONLY_FULL_GROUP_BY,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
transaction-isolation=READ-COMMITTED
```

5. Starting the MySQL Server

```
~]# systemctl  start mysqld
~]# systemctl  enable mysqld
```

6. Modify Root Password

```
~]# grep 'temporary password' /var/log/mysqld.log
2020-09-08T09:16:36.118277Z 1 [Note] A temporary password is generated for root@localhost: po_ni1-lwH,0
~]# mysql -uroot -p'po_ni1-lwH,0'
mysql>  ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';
~]# mysql -uroot -p'MyNewPass4!'
```

7. Database authorization

```
mysql> create database confluence default character set utf8 collate utf8_bin;
mysql> grant all on confluence.* to 'confluence'@'%' identified by 'confluence@PASS123';
mysql> flush privileges;
~]# mysql -uconfluence -p'confluence@ PASS123'
```

#### 安装  Confluence

```
~]#  wget https://product-downloads.atlassian.com/software/confluence/downloads/atlassian-confluence-7.2.0-x64.bin

```
