# mysql
detailed look into mysql

on unix check process with ```ps aux | grep mysql``` if instance of mysql not running ```/usr/bin/mysqld_safe &``` to start mysql deamon

shell ```mysql -u username -p```
set custom prompt to display default database ```prompt SQL Command \d>\_```

## new users & granting privleges

create:
```mysql
CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'new_password';
GRANT ALL PRIVILEGES ON dbTest.* To 'user'@'hostname' IDENTIFIED BY 'password';
```
grant privledges to particular statements - in this case ```SELECT```:
```mysql
GRANT SELECT ON *.* TO 'user'@'localhost';
```
grant all privleges:
```mysql
GRANT ALL ON *.* TO 'user'@'localhost';
```
view privleges:
```mysql
SHOW GRANTS FOR 'user'@'localhost';
```

## exploring databases

```mysql
CREATE DATABASE name;
```

```mysql
SHOW DATABASES;
```
- information_schema: server information
- mysql: user-names, passwords and privileges

set default:
```mysql
USE name
```

## tables

new:
```mysql
CREATE TABLE database_name.table_name (field_name DATA_TYPE, field_name DATA_TYPE...);
```
show:
```mysql
SHOW TABLES FROM database_name
```
show fields:
```mysql
DESCRIBE books
```

add field:
```mysql
ALTER TABLE name
ADD COLUMN column_name column_definition,
ADD COLUMN column_name column_definition,
...;
```

remove column:
```mysql
ALTER TABLE table
DROP COLUMN column_name;
```

## data

insert:
```mysql
INSERT INTO table_name VALUES(id, name, status)
```

```\G``` will present data in a batch of lines for each record format
select:
```mysql
SELECT * FROM table WHERE? field = val
```

update:
```mysql
UPDATE table SET field = val, field = val WHERE id = val;
```

join:
```mysql
SELECT book_id, title, status_name
FROM books JOIN status_names
WHERE status = status_id;
```
-  name specific columns between two tables
-  specify tables to join
-  match values of status column from books to the values of status_id column from status_names table


## variables

```mysql
SHOW VARIABLES LIKE 'variable_name';
SET GLOBAL variable_name = 6;
```


