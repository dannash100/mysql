## exercises

### chapter 1

1. Log into MySQL or MariaDB using the mysql client and switch the default database to the database, test. Create two tables called contacts and relation_types. For both tables, use column type INT for number columns and CHAR for character columns. Specify the maximum number of characters you want with CHAR—otherwise MySQL wills set a maximum of one character, which is not very useful. Make sure that you allow for enough characters to fit the data you will enter later. If you want to allow characters between numbers (e.g., hyphens for a telephone number), use CHAR. For the contacts, you will need six columns: name, phone_work, phone_mobile, email, relation_id. For the relation_types table, there should be only two columns: relation_id and relationship.
When you’re finished creating both tables, use the DESCRIBE statement to see how they look.

```mysql
CREATE TABLE contacts (id INT, name CHAR(255), phone_work INT, phone_mobile INT, email CHAR(255), relation_id INT);

CREATE TABLE relation_types (relation_id INT, relationship CHAR(255));

DESCRIBE contacts;

DESCRIBE relation_types;
```

2. Enter data in the two tables created in the previous exercise. Enter data in the second table, relation_types first. Enter three rows of data in it. Use single-digit, sequential numbers for the first column, but the following text for the second column: Family, Friend, Colleague. Now enter data in the table named contacts. Enter at least five fictitious names, telephone numbers, and email addresses. For the last column, relation_id, enter single digits to correspond with the relation_id numbers in the table, relation_types. Make sure you have at least one row for each of the three potential values for relation_id.

```mysql
INSERT INTO relation_types VALUES(1, "Family"), (2, "Friend");

INSERT INTO contacts
VALUES (100, "Garry N", 23423, 2342342, "dogman100@gmail.com", 1),
VALUES (101, "Anna P", 25125, 2356277, "dogman200@gmail.com", 1)
...;

```

3. Execute two SELECT statements to retrieve all of the columns of data from both tables that you created and filled with data from the previous two exercises. Then run a SELECT statement that retrieves only the person’s name and email address from the table named contacts.

```mysql
SELECT * FROM contacts;
SELECT * FROM relation_types;

SELECT name, email FROM contacts
```

4. Change some of the data entered in the previous exercises, using the UPDATE statement. If you don’t remember how to do that, refer back to the examples in this chapter on how to change data in a table. First, change someone’s name or telephone number. Next, change someone’s email address and his or her relationship to you (i.e., relation_id). Do this in one UPDATE statement.

```mysql
UPDATE contacts SET name = "Dan Nash" Where id = 100;

UPDATE contacts SET email = "danster15@gmail.com", relation_id = 3 WHERE id = 100;
```

5. Run a SELECT statement that joins both tables created in the first exercise. Use the JOIN clause to do this (the JOIN clause was covered in this chapter, so look back at the example if you don’t remember how to use it). Join the tables on the common column named relation_id—this will go in the WHERE clause. To help you with this, here’s how the clauses for the tables should look:
```mysql
FROM contacts JOIN relation_types
WHERE contacts.relation_id = relation_types.relation_id
```
Select the columns name and phone_mobile, but only for contacts who are marked as a Friend—you’ll have to add this to the WHERE with AND. Try doing this based on the value of relation_id and then again based on the value of the relationship column.

```mysql
SELECT *
FROM contacts JOIN relation_types
WHERE contacts.relation_id = relation_types.relation_id

SELECT name, phone_mobile
FROM contacts JOIN relation_types
WHERE contacts.relation_id = relation_types.relation_id
AND relationship = "Friend";
```
