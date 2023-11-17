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
    columnn type(size),
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
### Select data from table
```
SELECT column1, column3 or *
FROM tableName
WHERE condition;
```
### Update column value
```
UPDATE tableName
SET columnName=value
WHERE condition;
```
### Add new column
```
ALTER TABLE tableName
ADD columnx type(size);
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