# Database
### Create database
```
CREATE DATABASE databaseName;
```
### Drop database
```
DROP DATABASE databaseName;
```
### Show all databeses
```
SHOW DATABASE; 
```
# Table
### Creat Table
```
CREATE TABLE tableName(
    column1 type(size),
    ...
    columnn type(size) NOT NULL,
    PRIMARY KEY (columnx)
);
```
### Drop table
```
DROP TABLE tableName;
```
### Rename Table
```
RENAME TABLE oldTable to newTable;
```
# DML
### Insert data into table.
```
INSERT INTO tableName 
(column1, ..., columnn)
VALUES(value1, ..., valuen);
```
### Delete record
```
DELETE FROM tableName
WHERE condition;
```
### Select data from table
```
SELECT column1, column3 or *
FROM tableName
WHERE condition;
```
### Select distinct value
```
SELECT DISTINCT columnName
FROM tableName;
```
### Data sorting
```
SELECT gpa
FROM student
ORDER BY gpa DESC;
```
### Between
```
SELECT id, name
FROM student
WHERE id BETWEEN 5 and 10;
```
### IN
```
SELECT id, name
FROM student
WHERE id IN(5, 8, 3);
```
### Like
```
SELECT id, name
FROM student
WHERE name LIKE '_____AL%';
```
### Alias
```
SELECT id as Roll, name
FROM student;
```
### Update column value
```
UPDATE tableName
SET columnName=value
WHERE condition;
```
### Add/Delete new column
```
ALTER TABLE tableName
ADD columnx type(size)
DELETE columny;
```
### Rename Column
```
ALTER TABLE tableName
CHANGE oldcolumn_name new_columname type(size);
```
### Delete column
```
ALTER TABLE tableName
DROP COLUMN columnName;
```
### Group by column 
```
SELECT columnName
FROM tableName
GROUP BY columnName;
```
### Delete all data from table
```
TRUNCATE TABLE tableName;
```
# Join Table
### Show information from both tables
```
SELECT student.Roll, student.Name, result.reg, result.gpa
FROM student, result
WHERE student.Roll=result.ID;
```
Or
```
SELECT student.Roll, student.Name, result.reg, result.gpa
FROM student JOIN result
ON student.Roll=result.ID;
```
Or Inner join
```
SELECT student.Roll, student.Name, result.reg, result.gpa
FROM student INNER JOIN result
ON student.Roll=result.ID;
```
### Left/Right join
```
SELECT student.Roll, student.Name, result.reg, result.gpa
FROM student LEFT/Right JOIN result
ON student.Roll=result.ID;
```
### Combine two table (Union/Union All)
```
SELECT Roll, Name
FROM schoolStudent
UNION
SELECT Roll, Name
FROM collegeStudent;
```
# Date and time
```
SELECT CURDATE(), CURTIME();
```
or 
```
SELECT NOW();
```


# [Sources](https://youtu.be/aZnwpMON0NA?si=xsxKUiesnuLZX7gC)