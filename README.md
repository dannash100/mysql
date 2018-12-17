# mysql
detailed look into mysql

on unix check process with ```ps aux | grep mysql``` if instance of mysql not running ```/usr/bin/mysqld_safe &``` to start mysql deamon

shell ```mysql -u username -p```
set custom prompt to display default database ```prompt mysql \d ->\_```


## users & privileges

#### new user
```mysql
CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'new_password';
GRANT ALL PRIVILEGES ON dbTest.* To 'user'@'hostname' IDENTIFIED BY 'password';
```

#### granting privileges
grant privileges to particular statements - in this case ```SELECT```:
```mysql
GRANT SELECT ON *.* TO 'user'@'localhost';
```
grant all privileges:
```mysql
GRANT ALL ON *.* TO 'user'@'localhost';
```
view privileges:
```mysql
SHOW GRANTS FOR 'user'@'localhost';
```

#### variables

```mysql
SHOW VARIABLES LIKE 'variable_name';
SET GLOBAL variable_name = 6;
```


## exploring databases

#### create/remove
```mysql
CREATE DATABASE name
CHARACTER SET latin1
COLLATE latin1_bin;
```
- set default characters
- set default method of sorting data in tables based on binary latin characters

```mysql
DROP DATABASE name;
```
```mysql
SHOW DATABASES;
```
- information_schema: server information
- mysql: user-names, passwords and privileges

#### set default database
```mysql
USE name
```

## exploring tables

- the specification of fields and columns of a table is referred to as its schema
- when using CHAR or VARCHAR data types a maximum length must be specified otherwise it will default at 1
- columns may also specify how the data is indexed

#### create
```mysql
CREATE TABLE database_name.table_name (field_name DATA_TYPE, field_name DATA_TYPE...);
```

#### show
```mysql
SHOW TABLES FROM database_name
```

show fields:
```mysql
DESCRIBE books
```

#### add/remove column
```mysql
ALTER TABLE name
ADD COLUMN column_name column_definition,
ADD COLUMN column_name column_definition,
...;

ALTER TABLE table
DROP COLUMN column_name;
```

## data

#### types and indexing

##### VARCHAR vs CHAR
- if storage engine knows exactly what to expect from a column tables run faster can be indexed easier with CHAR
- when the width varies use VARCHAR - storage engine will reduce size of the column based on width

common auto incrementing id field
```mysql
id INT AUTO_INCREMENT PRIMARY KEY
```

```mysql
name VARCHAR(255) UNIQUE
```

#### insert
```mysql
INSERT INTO table_name VALUES(id, name, status)
```

```\G``` will present data in a batch of lines for each record format
select:
```mysql
SELECT * FROM table WHERE? field = val
```

#### update
```mysql
UPDATE table SET field = val, field = val WHERE id = val;
```

#### join
```mysql
SELECT book_id, title, status_name
FROM books JOIN status_names
WHERE status = status_id;
```
-  name specific columns between two tables
-  specify tables to join
-  match values of status column from books to the values of status_id column from status_names table

#### chaining where clauses
```mysql
AND field = value
```
for example to add an extra clause after a table join:
```mysql
FROM table JOIN table2
WHERE table.id = table2.id
AND field = value;
```


