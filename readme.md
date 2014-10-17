# Apartment lab

- Create a database called apartmentlab 
- Using this database, create two tables, one for owners and one for properties
- Keep this relationship in mind when designing your schema:
	+ **One owner can have many properties**

###Tables

- The owners table should consist of: 
	+ owner_id (this should be the primary key as well as a unique number that increments automatically)
	+ name
	+ age
- The properties table should consist of:
	+ property_id (this should be the primary key as well as a unique number that increments automatically)
	+ name
	+ number of units
	+ owner_id (this should have the constraint NOT NULL)
		+ There should be also be a foreign key that references the owners table

###Questions
Write down the following sql statements that are required to solve the following tasks.

```    
1. Show all the tables.

\dt

2. Show all the users. 

\du

3. Show all the data in the owners table.

MattM=# SELECT * FROM owners;
 owner_id |   name   | age 
----------+----------+-----
        1 | Patrick  |  61
        2 | Jennifer |  34
        3 | Dan      |  36
        4 | Matt     |  28
(4 rows)

4. Show the names of all owners. 

MattM=# SELECT name FROM owners;
   name   
----------
 Patrick
 Jennifer
 Dan
 Matt
(4 rows)

5. Show the ages of all of the owners in ascending order. 

MattM=# SELECT * FROM owners ORDER BY age ASC;                                                                                                                                    
 owner_id |   name   | age 
----------+----------+-----
        4 | Matt     |  28
        2 | Jennifer |  34
        3 | Dan      |  36
        1 | Patrick  |  61
(4 rows)

6. Show the name of an owner whose name is Donald. 

MattM=# SELECT * FROM owners WHERE name = 'Donald';                                                                                                                                 
 owner_id |  name  | age 
----------+--------+-----
        5 | Donald |  45
(1 row)

7. Show the age of all owners who are older than 30.

MattM=# SELECT * FROM owners WHERE age > 30;
 owner_id |   name   | age 
----------+----------+-----
        1 | Patrick  |  61
        2 | Jennifer |  34
        3 | Dan      |  36
        5 | Donald   |  45
(4 rows)

8. Show the name of all owners whose name contains an E.

MattM=# SELECT * FROM owners WHERE name LIKE '%e%';
 owner_id |   name   | age 
----------+----------+-----
        2 | Jennifer |  34
(1 row)

9. Add an owner named John who is 33 years old to the owners table.

MattM=# SELECT * FROM owners WHERE name = 'John';
 owner_id | name | age 
----------+------+-----
        6 | John |  33
(1 row)

10. Add an owner named Jane who is 43 years old to the owners table. 

MattM=# SELECT * FROM owners WHERE name = 'Jane';
 owner_id | name | age 
----------+------+-----
        7 | Jane |  43
(1 row)

11. Change Jane's age to 30. 

MattM=# SELECT * FROM owners WHERE name = 'Jane';
 owner_id | name | age 
----------+------+-----
        7 | Jane |  30
(1 row)

12. Change Jane's name to Janet. 

MattM=# SELECT * FROM owners WHERE name = 'Janet';
 owner_id | name  | age 
----------+-------+-----
        7 | Janet |  30
(1 row)

13. Add a property named Archstone that has 20 units. 

MattM=# SELECT * FROM properties;
 property_id |   name    | number_of_units | owner_id 
-------------+-----------+-----------------+----------
           6 | Archstone |              20 |        1
(1 row)

14. Delete the owner named Janet.

MattM=# DELETE FROM owners WHERE name = 'Janet';

DELETE 1
MattM=# SELECT * FROM owners;
 owner_id |   name   | age 
----------+----------+-----
        1 | Patrick  |  61
        2 | Jennifer |  34
        3 | Dan      |  36
        4 | Matt     |  28
        5 | Donald   |  45
        6 | John     |  33
(6 rows)

15. Show all of the properties in alphabetical order that are not named Archstone and do not have an id of 3 or 5.

MattM=# SELECT * FROM properties WHERE property_id NOT IN (3, 5) AND name NOT LIKE 'Archstone' ORDER BY name ASC;
 property_id |     name      | number_of_units | owner_id 
-------------+---------------+-----------------+----------
           7 | Campus Town   |              30 |        2
           9 | Humphrey Hall |              40 |        9
           8 | Roseneth      |               6 |        8
(3 rows)


16. Count the total number of rows in the properties table.

MattM=# SELECT COUNT(*) FROM properties;
 count 
-------
     4
(1 row

17. Show the highest age of all owners.

MattM=#  SELECT MAX(age) FROM owners;
 max 
-----
  61
(1 row)

18. Show the names of the first three owners in your owners table.

MattM=# SELECT * FROM owners LIMIT 3;
 owner_id |   name   | age 
----------+----------+-----
        1 | Patrick  |  61
        2 | Jennifer |  34
        3 | Dan      |  36
(3 rows)

19. Create a foreign key that references the owner_id in the owners table and forces the constraint ON DELETE NO ACTION. 

MattM=# ALTER TABLE properties ADD CONSTRAINT owner_fk FOREIGN KEY (owner_id)REFERENCES owners (owner_id) ON DELETE NO ACTION;
ALTER TABLE

20. Show all of the information from the owners table and the properties table in one joined table.  

MattM=# SELECT * FROM owners FULL OUTER JOIN properties ON owners.owner_id = properties.owner_id;
 owner_id |   name   | age | property_id |     name      | number_of_units | owner_id 
----------+----------+-----+-------------+---------------+-----------------+----------
        1 | Patrick  |  61 |           6 | Archstone     |              20 |        1
        2 | Jennifer |  34 |           7 | Campus Town   |              30 |        2
          |          |     |           8 | Roseneth      |               6 |        8
          |          |     |           9 | Humphrey Hall |              40 |        9
        5 | Donald   |  45 |             |               |                 |         
        6 | John     |  33 |             |               |                 |         
        4 | Matt     |  28 |             |               |                 |         
        3 | Dan      |  36 |             |               |                 |         
(8 rows)

```
Bonus (this might require you to look up documentation online)

```
1. In the properties table change the name of the column "name" to "property_name". 



2. Count the total number of properties where the owner_id is between 1 and 3.
```
