# mysql
detailed look into mysql

on unix check process with ```ps aux | grep mysql``` if instance of mysql not running ```/usr/bin/mysqld_safe &``` to start mysql deamon

shell ```mysql -u root -p -e```

## new users & granting privleges

create
```mysql
CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'new_password';
GRANT ALL PRIVILEGES ON dbTest.* To 'user'@'hostname' IDENTIFIED BY 'password';
```
grant privledges to particular statements - in this case ```SELECT```:
```mysql
GRANT SELECT ON *.* TO 'user'@'localhost';" 
```
grant all privleges:
```mysql
GRANT ALL ON *.* TO 'user'@'localhost';
```
view privleges
```mysql
SHOW GRANTS FOR 'user'@'localhost';
```

## variables

```mysql
SHOW VARIABLES LIKE 'variable_name';
SET GLOBAL variable_name = 6;
```
