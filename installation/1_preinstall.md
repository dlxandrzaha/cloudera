#<center> Pre-Install
## <center> MySQL
**Note:** Using RHEL 7.2 yet mariadb failed to start at all. Bebugin the issue did not help. Instead MySQL was used.
**ISSUE:** ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)

Stack overflow and other resource solutions did not work

* Pull repo
	* Used WGET to pull RHEL 7 mysql repo
`$ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm`
* Add REPO
`$ rpm -ivh mysql-community-release-el7-5.noarch.rpm`
* Install MySQL server
`$ yum install mysql-server`
* Start MySQL server
`$ systemctl start mysqld`
* Run script (configure)
`$ mysql_secure_installation`
* Dowloand jdbc connector
`$ wget http://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-5.1.39.tar.gz`
* Check dir
`$ /usr/share/`
* Create dir
`$ mkdir /usr/share/java`
* Unzip gz
`$ tar zxvf mysql-connector-java-5.1.39.tar.gz`
* Move JDBC connector
`$ cp mysql-connector-java-5.1.39/mysql-connector-java-5.1.39-bin.jar /usr/share/java/mysql-connector-java.jar'
* Check
`$ ll /usr/share/java/`
* Create database script
`$ vi db_prep.sql`
* Add queries
```
create database amon DEFAULT CHARACTER SET utf8;
create database rman DEFAULT CHARACTER SET utf8;
create database metastore DEFAULT CHARACTER SET utf8;
create database sentry DEFAULT CHARACTER SET utf8;
create database nav DEFAULT CHARACTER SET utf8;
create database navms DEFAULT CHARACTER SET utf8;
grant all on database.amon TO 'amon'@'%' IDENTIFIED BY 'amon_password';
grant all on database.rman TO 'rman'@'%' IDENTIFIED BY 'rman_password';
grant all on database.metastore TO 'hive'@'%' IDENTIFIED BY 'hive_password';
grant all on database.sentry TO 'sentry'@'%' IDENTIFIED BY 'sentry_password';
grant all on database.nav TO 'nav'@'%' IDENTIFIED BY 'nav_password';
grant all on database.navms TO 'navms'@'%' IDENTIFIED BY 'navms_password';
```
* Run script
`$ mysql -u root -p < db_prep.sql
* Check databases
`$ mysql -u root -p`
`$ show databases;`
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| amon               |
| metastore          |
| mysql              |
| nav                |
| navms              |
| performance_schema |
| rman               |
| sentry             |
+--------------------+
9 rows in set (0.00 sec)
```
`$ exit;`
* Check new user
`$ mysql -u amon -p`
```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 27
Server version: 5.6.31 MySQL Community Server (GPL)
Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

## Install Cloudera Manager (CM)
### Python
* Python 2.7 is pre-installed on RHEL 7.2

### Java
* Download Oracle JDK
	* Used rpm for RHEL
	* Downloaded from Oracle website
	* Version - 7u80
	* Pushed to server with SFTP
* Install JDK
`$ rpm -ivh jdk-7u80-linux-x64.rpm`
* Check version
` $ java -version`
```
java version "1.7.0_80"
Java(TM) SE Runtime Environment (build 1.7.0_80-b15)
Java HotSpot(TM) 64-Bit Server VM (build 24.80-b11, mixed mode)
```
* Add PATH
`$ export JAVA_HOME=/usr/java/jdk1.7.0_80`
`$ export PATH=$PATH:$JAVA_HOME`
`$ echo $JAVA_HOME`
```
/usr/java/jdk1.7.0_80
```
* Make persisent
`$ vi /etc/profile.d/java.sh`
* Add script
```
#!/bin/bash
JAVA_HOME=/usr/java/jdk1.7.0_80/
PATH=$JAVA_HOME/bin:$PATH
export PATH JAVA_HOME
export CLASSPATH=.
```
* Make executable
`$ chmod +x /etc/profile.d/java.sh`
* Set permanent
`$ source /etc/profile.d/java.sh`

### 

## Parcels
* Get manifest.json file
`$ wget http://archive.cloudera.com/cdh5/parcels/latest/manifest.json`
* Get parces "CDH-5.7.1-1.cdh5.7.1.p0.11-el7.parcel"
`$ wget https://archive.cloudera.com/cdh5/parcels/5.7.1.11/CDH-5.7.1-1.cdh5.7.1.p0.11-el7.parcel`
* Make new dir
` mkdir /var/www/html/cdh5.7`
* Move parcel
`$ mv CDH-5.7.1-1.cdh5.7.1.p0.11-el7.parcel /var/www/html/cdh5.7`
* Move manifest
`$ mv manifest.json /var/www/html/cdh5.7`
* Check hosted parcel (in web-browser)
`$ http://ec2-52-208-1-52.eu-west-1.compute.amazonaws.com/cdh5.7/'
