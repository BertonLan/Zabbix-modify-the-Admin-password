# Zabbix-modify-the-Admin-password
```
[root@localhost ~]# mysql -uroot -p
password
mysql> show databases;
mysql> use zabbix;
mysql> show tables;
mysql> select * from users;
+--------+-------+--------+---------------+----------------------------------+-----+-----------+------------+-------+---------+------+---------+----------------+------------+---------------+---------------+
| userid | alias | name   | surname       | passwd                           | url | autologin | autologout | lang  | refresh | type | theme   | attempt_failed | attempt_ip | attempt_clock | rows_per_page |
+--------+-------+--------+---------------+----------------------------------+-----+-----------+------------+-------+---------+------+---------+----------------+------------+---------------+---------------+
|      1 | Admin | Zabbix | Administrator | 5fce1b3e34b520afeffb37ce08c7cd66 |     |         1 | 0          | zh_CN | 30s     |    3 | default |              0 |            |             0 |            50 |
|      2 | guest |        |               | d41d8cd98f00b204e9800998ecf8427e |     |         0 | 15m        | en_GB | 30s     |    1 | default |              0 |            |             0 |            50 |
+--------+-------+--------+---------------+----------------------------------+-----+-----------+------------+-------+---------+------+---------+----------------+------------+---------------+---------------+
mysql> select userid,passwd from users; 
+--------+----------------------------------+
| userid | passwd                           |
+--------+----------------------------------+
|      1 | 5fce1b3e34b520afeffb37ce08c7cd66 |
|      2 | d41d8cd98f00b204e9800998ecf8427e |
+--------+----------------------------------+
mysql> quit;
[root@localhost ~]# echo -n zabbix|openssl md5
(stdin)= 5fce1b3e34b520afeffb37ce08c7cd66
[root@localhost ~]# mysql -uroot -p
mysql> update users set passwd='5fce1b3e34b520afeffb37ce08c7cd66' where userid = '1'; 
mysql> flush privileges; 
mysql> quit;
