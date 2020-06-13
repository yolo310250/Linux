# zabbix安裝與使用
```
rpm -Uvh https://repo.zabbix.com/zabbix/4.0/rhel/8/x86_64/zabbix-release-4.0-2.el8.noarch.rpm
```
## Mariadb安裝
```
yum -y install mariadb mariadb-server
systemctl start mariadb.service 
systemctl enable mariadb.service
```
## zabbix資料庫
```
mysqladmin -uroot password

mysql -uroot -pcentos 

create database zabbix character set utf8 collate utf8_bin;

grant all privileges on zabbix.* to zabbix@localhost identified by 'zabbix';

yum -y install zabbix-server-mysql zabbix-web-mysql zabbix-agent 

zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql (將初始資料表匯入 zabbix 資料庫)
```
cp /etc/zabbix/zabbix_server.conf /etc/zabbix/zabbix_server.conf.bak

vim /etc/zabbix/zabbix_server.conf 

91 DBHost=localhost <!--去掉注释符号--> 100 DBName=zabbix <!--数据库名称，根据实际修改，默认不用修改--> 116 DBUser=zabbix <!--数据库用户名，默认不用修改--> 124 DBPassword=zabbix <!--数据库密码，修改此行-->

vim /etc/zabbix/zabbix_agentd.conf 

98 Server=127.0.0.1 <!--客户端被动等待指定服务器来查询数据--> 139 ServerActive=127.0.0.1 <!--客户端主动提交数据到指定的服务器--> 150 Hostname=centos <!--建议修改此行，配置规范的主机名-->

vim /etc/httpd/conf.d/zabbix.conf 

php_value date.timezone Asia/Taipei

systemctl start zabbix-server.service

systemctl enable zabbix-server

systemctl start httpd

systemctl start zabbix-agent

systemctl enable zabbix-agent
