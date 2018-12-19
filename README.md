# mysql
detailed look into mysql

on unix check process with ```ps aux | grep mysql``` if instance of mysql not running ```/usr/bin/mysqld_safe &``` to start mysql daemon

open MySQL prompt: ```mysql -u username -p```
set custom prompt to display default database ```prompt mysql \d ->\_```

---

### data precautions

#### mysqldump
- utility to make backup of tables
- database name is given then optionally followed by a table name.
- (>) tells the shell to send results of the dump to text file table_name.sql

backup
```console
mysqldump --user='dannash100' -p \
database_name table_name > ~/tmp/backup.sql
```

restore *note: use mysql not mysqldump*
```console
mysql --user='dannash100' -p \
database_name < backup.sql
```

---

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

---


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

---

## exploring tables

- the specification of fields and columns of a table is referred to as its schema
- when using CHAR or VARCHAR data types a maximum length must be specified otherwise it will default at 1
- columns may also specify how the data is indexed

#### create
```mysql
CREATE TABLE database_name.table_name (field_name DATA_TYPE, field_name DATA_TYPE...);
```

#### create with copied columns
```mysql
CREATE TABLE tab_name
SELECT col, col2
FROM tab_to_copy_from
```

#### show
```mysql
SHOW TABLES FROM database_name
```

show fields:
```mysql
DESCRIBE books
```

show information specified in table creation:
```mysql
SHOW CREATE TABLE name \G
```


#### add/remove/edit column
```mysql
ALTER TABLE name
ADD COLUMN column_name column_definition AFTER column_to_fall_after,
ADD COLUMN column_name column_definition,
...;
ALTER TABLE name
DROP COLUMN column_name;

ALTER TABLE name
CHANGE COLUMN column_name new_name NEW_TYPE;

```

#### copy table
1st method is preferred as it copies table settings.
```mysql
CREATE TABLE new_table LIKE table_to_copy;

INSERT INTO new_table
SELECT * FROM table_to_copy;

CREATE TABLE new_table SELECT * FROM table_to_copy;
```

---

## data

### types and indexing

#### view columns in detail
```mysql
SHOW COLUMNS FROM tab LIKE 'col' \G
```

#### default values
```mysql
INT DEFAULT 8;

ALTER TABLE tab
AlTER col SET DEFAULT 7;
ALTER col DROP DEFAULT;

```

#### ENUMS
```mysql
ENUM('option', 'option'...)
```
first value is index 1

#### VARCHAR vs CHAR
- if storage engine knows exactly what to expect from a column tables run faster can be indexed easier with CHAR
- when the width varies use VARCHAR - storage engine will reduce size of the column based on width

#### large strings
- use TEXT to hold up to 65,535 bytes of data

#### image files
- use BLOB or binary large object to store image file such as jpeg, although it is preferable to store image files on a server, or as a url address in the database.

#### null values
- null setting indicates whether each field may contain NULL values.

#### common settings
```mysql
id INT AUTO_INCREMENT PRIMARY KEY
```

```mysql
name VARCHAR(255) UNIQUE
```

if names include characters not part of default latin1 char set
```mysql
CREATE TABLE table_name ( fields ) DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;
```

### modify/change fields

change type w/o rename
```mysql
ALTER TABLE t1 MODIFY col1 BIGINT;
```
change with rename
```mysql
ALTER TABLE t1 CHANGE a b BIGINT NOT NULL;
```

### interacting with data

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

UPDATE table SET field = val, field = val WHERE id IN(val, val, val, val);

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

#### where/wherenot

add an extra clause after a table join:
```mysql
FROM table JOIN table2
WHERE table.id = table2.id
AND field = value;
```

select all where not
```mysql
SELECT * from table_name
WHERE NOT field = val;
```

#### order

```mysql
SELECT * FROM tab
ORDER BY col;
```

#### indexes

also referred to as keys - indexes are used by mysql to locate data quickly. Indexs derive from referenced columns and allow mysql to search more efficiently for data than sequentially processing the entries of a table.

if you try to use ALTER TABLE on a column that is indexed you will get an error message.
use:
```mysql
ALTER TABLE tab
DROP PRIMARY KEY
CHANGE old_name new_name INT PRIMARY KEY AUTO_INCREMENT;
```

```mysql
Alter TABLE tab
ADD INDEX idx_name (col_to_index, col_to_index);

SHOW INDEX FROM tab
WHERE Key_name = 'idx_name' \G
```



