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
