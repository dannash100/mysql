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

#### chapter 5

1. Earlier in this chapter, we created a table called birds_details. We created the table with two columns: bird_id and description. We took these two columns from the birds table. Our intention in creating this table was to add columns to store a description of each bird, notes about migratory patterns, areas in which they can be found, and other information helpful in locating each bird in the wild. Let’s add a couple of columns for capturing some of that information.
Using the ALTER TABLE statement, alter the birds_details table. In one SQL statement, add two columns named migrate and bird_feeder, making them both integer (INT) columns. These will contain values of 1 or 0 (i.e., Yes or No). In the same SQL statement, using the CHANGE COLUMN clause, change the name of the column, description to bird_description.
When you’re finished altering the table, run the SHOW CREATE TABLE statement for this table to see the results.
ffsd
```mysql
  ALTER TABLE birds_details
  ADD migrate INT(1), ADD bird_feeder INT(1)
  CHANGE description bird_description TEXT;

  SHOW CREATE TABLE birds_details \G
```

2. Using the CREATE TABLE statement, create a new reference table named, habitat_codes. Create this table with two columns: name the first column habi tat_id and make it a primary key using AUTO_INCREMENT and the column type of INT. Name the second column habitat and use the data type VARCHAR(25). Enter the following SQL statement to add data to the table:
```mysql
  INSERT INTO habitat_codes (habitat) VALUES('Coasts'), ('Deserts'), ('Forests'), ('Grasslands'), ('Lakes, Rivers, Ponds'), ('Marshes, Swamps'), ('Mountains'), ('Oceans'), ('Urban');
```
  Execute a SELECT statement for the table to confirm that the data was entered correctly. It should look like this:

  | habitat_id    | habitat       |
  | ------------- |:-------------:|
  | 1     | Coasts |
  | 2      | Deserts      |
  | 3 | Forests      |
  | 4 | Grasslands |
  | 5 | Lakes, Rivers, Ponds |
  | 6 | Marshes, Swamps |
  | 7 | Mountains |
  | 8 | Oceans |
  | 9 | Urban |

  Create a second table named bird_habitats. Name the first column bird_id and the second column habitat_id. Set the column type for both of them to INT. Don’t make either column an indexed column.
  When you’re finished creating both of these tables, execute the DESCRIBE and SHOW CREATE TABLE statements for each of the two tables. Notice what information is presented by each statement, and familiarize yourself with the structure of each table and the components of each column.
  Use the RENAME TABLE statement to rename the bird_habitats to birds_habitats (i.e., make bird plural). This SQL statement was covered in “Renaming a Table” on page 77.

```mysql
CREATE TABLE habitat_codes (
  habitat_id INT AUTO_INCREMENT PRIMARY KEY,
  habitat VARCHAR(25)
);

CREATE TABLE bird_habitats (
  bird_id INT,
  habitat_id INT
);

ALTER TABLE bird_habitats
RENAME birds_habitats;
```

3. Using the ALTER TABLE statement, add an index based on both bird_id and the habitat_id columns combined (this was covered in “Indexes” on page 80). Instead of using the INDEX keyword, use UNIQUE so that duplicates are not allowed. Call the index birds_habitats.
Execute the SHOW CREATE TABLE statement for this table when you’re finished altering it.
At this point, you should enter some data in the birds_habitats table. Execute these two SELECT statements, to see what data you have in the birds and habitat_codes tables:
```mysql
SELECT bird_id, common_name FROM birds;
SELECT * FROM habitat_codes;
```
  The results of the first SELECT statement should show you a row for a loon and one for a duck, along with some other birds. Both the loon and the duck can be found in lakes, but ducks can also be found in marshes. So enter one row for the loon and two rows for the duck in the birds_habitats table. Give the value of the bird_id for the loon, and the value of habitat_id for Lakes, Rivers, Ponds. Then enter a row giving the bird_id for the duck, and the value again of the habitat_id for lakes. Then enter a third row giving again the bird_id for the duck and this time the habitat_id for Marshes, Swamps. If you created the index properly, you should not get an error about duplicate entries. When you’re done, execute the SELECT statement to see all of the values of the table.
