# MySQL
**Note:** Using RHEL 7.2 yet mariadb failed to start at all. Bebugin the issue did not help. Instead MySQL was used.
**ISSUE:** ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)

Stack overflow and other resource solutions did not work

* Pull repo
	* Used WGET to pull RHEL 7 mysql repo
`$ wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm`
* Add REPO
`$ rpm -ivh mysql-community-release-el7-5.noarch.rpm`
* Install MySQL
`$ yum install mysql-server`
* Start MySQL server
`$ systemctl start mysqld`
* Run script (configure)
`$ mysql_secure_installation`
