## exercises

### part 3. basics of handling data

#### chapter 6

1. In the exercises at the end of Chapter 4, you were asked to create a table called birds_body_shapes. This table will be used for identifying birds. It will be referenced from the birds table by way of the column called body_id. The table is to contain descriptions of body shapes of birds, which is a key factor in identifying birds: if it looks like a duck, walks like a duck, and quacks like a duck, it may be a goose — but it’s definitely not a hummingbird. Here is an initial list of names for general shapes of birds:
Hummingbird
Long-Legged Wader
Marsh Hen
Owl
Perching Bird
Perching Water Bird Pigeon
Raptor
Seabird
Shore Bird
Swallow
Tree Clinging
Waterfowl
Woodland Fowl

Construct an INSERT statement using the multiple-row syntax—not the emphatic method—for inserting data into the birds_body_shapes table. You’ll have to set the body_id to a three-letter code. You decide on that, but you might base it somewhat on the names of the shapes themselves (e.g., Marsh Hen might be MHN and Owl might be simply OWL). Just make sure each ID is unique. For the body_shape column, use the text I have just shown, or reword it if you want. For now, skip the third column, body_example.


```mysql
INSERT INTO bird_body_shapes(body_id, body_shape) Values
('HMB', 'Hummingbird'),
('LLW', 'Long-Legged Wader'),
('MSH', 'Marsh Hen'),
('OWL', 'Owl'),
('PCB', 'Perching Bird'),
('PWP', 'Perching Water Bird Pigeon'),
('RPT', 'Raptor'),
('SEA', 'Seabird'),
('SHR', 'Shore Bird'),
('SWL', 'Swallow'),
('TRC', 'Tree Clinging'),
('WTF', 'Waterfowl'),
('WOF', 'Woodland Fowl');
```

2. You were asked also in the exercises at the end of Chapter 4 to create another table for identifying birds, called birds_wing_shapes. This describes the shapes of bird wings. Here’s an initial list of names for general wing shapes:
Broad
Rounded
Pointed
Tapered
Long
Very Long
Construct an INSERT statement to insert these items into the birds_wing_shapes table using the emphatic syntax—the method that includes the SET clause. Set the wing_id to a two-letter code. You decide these values, as you did earlier for body_id. For the wing_shape column, use the text just shown. Don’t enter a value for the wing_example column yet.


```mysql
INSERT INTO bird_wing_shapes
SET wing_id = 'BR',
wing_shape = 'Broad';

INSERT INTO bird_wing_shapes
SET wing_id = 'RO',
wing_shape = 'Rounded';

INSERT INTO bird_wing_shapes
SET wing_id = 'TA',
wing_shape = 'Tapered';
```

3. The last bird identification table in which to enter data is birds_bill_shapes. Use the INSERT statement to insert data into this table, but whichever multiple-row method you prefer. You determine the two-letter values for bill_id. Don’t enter values for bill_example. Use the following list of bill shapes for the value of bill_shape:
All Purpose
Cone
Curved
Dagger
Hooked
Hooked Seabird
Needle
Spatulate
Specialized

```mysql
INSERT INTO bird_bill_shapes(bill_id, bill_shape) Values
('AL', 'All Purpose'),
('CO', 'Cone'),
('CU', 'Curved'),
('DA', 'Dagger'),
('HO', 'Hooked'),
('NE', 'Needle'),
('SA', 'Spatulate'),
('SE', 'Specialized');
```

4. Execute a SELECT statement to view the row from the birds_body_shapes table where the value of the body_shape column is Woodland Fowl. Then replace that row with a new value for the body_shape column. Replace it with Upland Ground Birds. To do this, use the REPLACE statement, covered in “Replacing Data” on page 110. In the VALUES clause of the REPLACE statement, provide the same value previ‐ ously set for the body_id so that it is not lost.
After you enter the REPLACE statement, execute a SELECT statement to retrieve all the rows of data in the birds_body_shapes table. Look how the data changed for the row you replaced. Make sure it’s correct. If not, try again either using REPLACE or UPDATE.


```mysql
SELECT * FROM bird_body_shapes
WHERE body_shape = 'Woodland Fowl';

REPLACE INTO bird_body_shapes(body_id, body_shape)
VALUES('WOF', 'Upland Ground Birds');
```


#### chapter 7

1. Construct a SELECT statement to select the common names of birds from the birds table. Use the LIKE operator to select only Pigeons from the table. Order the table by the common_name column, but give it a field alias of Bird'. Don’t limit the results; let MySQL retrieve all of the rows that match. Execute the statement on your server and look over the results.
Next, use the same SELECT statement, but add a LIMIT clause. Limit the results to the first ten rows and execute it. Compare the results to the previous SELECT statement to make sure the results show the 1st through 10th row. Then modify the SELECT statement again to display the next 10 rows. Compare these results to the results from the first SELECT statement to make sure you retrieved the 11th through 20th row. If you didn’t, find your mistake and correct it until you get it right.

```mysql
SELECT common_name as 'Bird'
WHERE common_name LIKE '%Pigeon'
ORDER BY Bird;

SELECT common_name as 'Bird'
WHERE common_name LIKE '%Pigeon'
ORDER BY Bird
LIMIT 10;

SELECT common_name as 'Bird'
WHERE common_name LIKE '%Pigeon'
ORDER BY Bird
LIMIT 20, 10;
```

2. In this exercise, you’ll begin with a simple SELECT statement and then make it more complicated. To start, construct a SELECT statement in which you select the scientific_name and the brief_description from the bird_orders table. Give the field for the scientific_name an alias of Order—and don’t forget to put quotes around it because it’s a reserved word. Use an alias of Types of Birds in Order for brief_description. Don’t limit the results. When you think that you have the SELECT statement constructed properly, execute it. If you have errors, try to determine the problem and fix the statement until you get it right.
Construct another SELECT statement in which you retrieve data from the birds table. Select the common_name and the scientific_name columns. Give them field aliases: Common Name of Bird and Scientific Name of Bird. Exclude rows in which the common_name column is blank. Order the data by the common_name column. Limit the results to 25 rows of data. Execute the statement until it works without an error.
Merge the first and second SELECT statements together to form one SELECT statement that retrieves the same four columns with the same alias from the same two tables (this was covered in “Combining Tables” on page 124). It involves giving more than one table in the FROM clause and providing value pairs in the WHERE clause for temporarily connecting the tables to each other. This one may seem tricky. So take your time and don’t get frustrated. If necessary, refer back to “Combining Tables” on page 124.

```mysql
SELECT scientific_name AS 'Order', brief_description AS 'Types of Birds'
FROM bird_orders;

SELECT common_name AS 'Common Name of Bird', scientific_name as 'Scientific Name of Bird'
FROM birds
WHERE common_name != ""
ORDER BY common_name
LIMIT 25

SELECT orders.scientific_name AS 'Order', orders.brief_description AS 'Types of Birds',
common_name AS 'Common Name of Bird', birds.scientific_name as 'Scientific Name of Bird'
FROM birds, bird_orders as orders, bird_families as families
WHERE birds.family_id = families.family_id
AND families.order_id = orders.order_id
AND common_name != ""
ORDER BY common_name LIMIT 10;
```

3. Use the SELECT statement in conjunction with REGEXP in the WHERE clause to get a list of birds from the birds table in which the common_name contains the word “Pigeon” or “Dove” (this was covered in “Expressions and the Like” on page 127). Give the field for the common_name column the alias >Type of Columbidae—that’s the name of the family to which Doves and Pigeons belong.

```mysql
SELECT common_name as 'Type of Columbidae'
FROM birds
WHERE common_name REGEXP "Pigeon|Dove"
```
