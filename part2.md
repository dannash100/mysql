## exercises

### part 2. database structures

#### chapter 4

1. I mentioned in this chapter that we might want to store data related to identifying birds. Instead of putting that data in the birds table, create a table for that data, which will be a reference table. Try creating that table with the CREATE TABLE statement. Name it birds_wing_shapes. Give it three columns: the first column should be named wing_id with a data type of CHAR with the maximum character width set to 2. Make that column the index, as a UNIQUE key, but not an AUTO_INCREMENT. We’ll enter two-letter codes manually to identify each row of data a feasible task because there will be probably only six rows of data in this table. Name the second column wing_shape and set its data type to CHAR with the maximum character width set to 25. This will be used to describe the type of wings a bird may have (e.g., tapered wings). The third column should be called wing_example and make it a BLOB column for storing example images of the shapes of wings.

```mysql
create table bird_wing_shapes (
  wing_id char(2) unique,
  wing_shape char(25),
  wing_example blob
);
```

2. After creating the birds_wing_shapes table in the previous exercise, run the SHOW CREATE TABLE statement for that table in mysql. Run it twice: once with the semi-colon at the end of the SQL statement and another time with \G to see how the different displays can be useful given the results.
Copy the results of the second statement, the CREATE TABLE statement it returns. Paste that into a text editor. Then use the DROP TABLE statement to delete the table birds_wing_shapes in mysql.
In your text editor, change a few things in the CREATE TABLE statement you copied. First, change the storage engine—the value of ENGINE for the table—to a MyISAM table, if it’s not already. Next, change the character set and collation for the table. Set the character set to utf8 and the collation to utf8_general_ci.
Now copy the CREATE TABLE statement you modified in your text editor and paste it into the mysql monitor and press [Enter] to run it. If you get an error, look at the confusing error message and then look at the SQL statement in your text editor. Look where you made changes and see if you have any mistakes. Make sure you have keywords and values in the correct places and there are no typos. Fix any mistakes you find and try running the statement again. Keep trying to fix it until you’re successful. Once you’re successful, run the DESCRIBE statement for the table to see how it looks.

```mysql
DROP TABLE bird_wing_shapes;

CREATE TABLE bird_wing_shapes (
  `wing_id` char(2) COLLATE latin1_bin DEFAULT NULL,
  `wing_shape` char(25) COLLATE latin1_bin DEFAULT NULL,
  `wing_example` blob,
  UNIQUE KEY `wing_id` (`wing_id`)
) ENGINE=MyISAM DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

DESCRIBE bird_wing_shapes;
```

3. Create two more tables, similar to birds_wing_shapes. One table will store information on the common shapes of bird bodies, and the other will store information on the shapes of their bills. They will also be used for helping bird-watchers to identify birds. Call these two tables birds_body_shapes and birds_bill_shapes.
For the birds_body_shapes table, name the first column body_id, set the data type to CHAR(3), and make it a UNIQUE key column. Name the second column body_shape with CHAR(25), and the third column body_example, making it a BLOB column for storing images of the bird shapes.
For the birds_bill_shapes table, create three similar columns: bill_id with CHAR(2) and UNIQUE; bill_shape with CHAR(25); and bill_example, making it a BLOB column for storing images of the bird shapes. Create both tables with the ENGINE set to a MyISAM, the DEFAULT CHARSET, utf8, and the COLLATE as utf8_general_ci. Run the SHOW CREATE TABLE statement for each table when you’re finished to check your work.

```mysql
CREATE TABLE bird_body_shapes (
  body_id char(3) unique,
  body_shape char(25),
  body_example blob
) ENGINE=MyISAM DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

CREATE TABLE bird_bill_shapes (
  bill_id char(2) unique,
  bill_shape char(25),
  bill_example blob
) ENGINE=MyISAM DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

SHOW CREATE TABLE bird_body_shapes;
SHOW CREATE TABLE bird_bill_shapes;
```
