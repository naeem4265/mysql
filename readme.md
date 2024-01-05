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

# Practice

##### Write a query 
identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the Equilateral, Isosceles, Scalene or Not A Triangle
```
SELECT CASE WHEN ((A+B)<=C OR (B+C)<=A OR (A+C)<=B) THEN 'Not A Triangle' ELSE (CASE WHEN (A=B AND B=C) THEN 'Equilateral' WHEN ((A=B AND B!=C)OR (A=C AND A!=B) OR (B=C AND A!=B)) THEN 'Isosceles' ELSE 'Scalene' END ) END
FROM TRIANGLES;
```

##### Query the Name
 of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.
```
SELECT NAME 
FROM STUDENTS
WHERE MARKS > 75
ORDER BY RIGHT(NAME, 3) ASC, ID ASC;
```

##### Query 
the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.
```
(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) ASC, CITY ASC
LIMIT 1)
UNION ALL 
(SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY ASC
LIMIT 1);
```

##### Query
 an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S). 2.Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order.:
```
(SELECT CONCAT(Name, '(', LEFT(OCCUPATION, 1), ')' )
FROM OCCUPATIONS
ORDER BY NAME ASC);

(SELECT CONCAT('There are a total of ', COUNT(OCCUPATION), ' ', LOWER(OCCUPATION), 's.')
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(Name) ASC, OCCUPATION ASC);
```

##### We define an employee's total earnings to be their monthly  worked
, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as  space-separated integers.:
```
SELECT MAX(salary*months), COUNT( employee_id )
FROM Employee
WHERE (salary*months) = (SELECT MAX(salary*months) FROM Employee );
```

##### Query the sum of Northern Latitudes (LAT_N) 
from STATION having values greater than  and less than . Truncate your answer to  decimal places.
```
SELECT ROUND( SUM(LAT_N), 4 )
FROM STATION
WHERE LAT_N > 38.7880 AND LAT_N < 137.2345;
```

##### Query the Western Longitude (LONG_W)
where the smallest Northern Latitude (LAT_N) in STATION is greater than . Round your answer to  decimal places.
```
SELECT ROUND( LONG_W, 4 ) 
FROM STATION
WHERE LAT_N = ( SELECT MIN(LAT_N) FROM STATION WHERE LAT_N > 38.7780 );
```

##### Given the CITY and COUNTRY tables
query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.
```
SELECT COUNTRY.CONTINENT, FLOOR( AVG( CITY.POPULATION))
FROM CITY INNER JOIN COUNTRY
ON CITY.COUNTRYCODE = COUNTRY.CODE
GROUP BY COUNTRY.CONTINENT;
```

##### the-report
Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.
```
SELECT (CASE WHEN Marks < 70 THEN "NULL" ELSE Name END), (CASE WHEN Marks = 100 THEN 10 ELSE FLOOR(Marks/10)+1 END) AS G, Marks FROM Students
ORDER BY G DESC, Name ASC;
```

##### [New Company Dependencies](https://www.hackerrank.com/challenges/the-company/problem?isFullScreen=true)
```
SELECT Company.company_code, Company.founder, 
( SELECT COUNT( DISTINCT Lead_Manager.lead_manager_code ) FROM Lead_Manager WHERE Lead_Manager.company_code = Company.company_code ), 
( SELECT COUNT( DISTINCT Senior_Manager.senior_manager_code ) FROM Senior_Manager WHERE Senior_Manager.company_code = Company.company_code ), 
( SELECT COUNT( DISTINCT Manager.manager_code ) FROM Manager WHERE Manager.company_code = Company.company_code ), 
( SELECT COUNT( DISTINCT Employee.employee_code ) FROM Employee WHERE Employee.company_code = Company.company_code )
FROM Company
ORDER BY Company.company_code ASC;
```

##### [Top Competitors](https://www.hackerrank.com/challenges/full-score/problem?isFullScreen=true)
```
SELECT h.hacker_id, h.name
FROM Hackers AS h 
JOIN Submissions AS s ON h.hacker_id = s.hacker_id
JOIN Challenges AS ch ON s.challenge_id = ch.challenge_id
JOIN Difficulty AS d ON ch.difficulty_level = d.difficulty_level 
WHERE s.score = d.score

GROUP BY h.hacker_id, h.name
HAVING COUNT( s.submission_id ) > 1

ORDER BY COUNT( s.submission_id ) DESC, h.hacker_id ASC;
```

##### [Ollivander's Inventory](https://www.hackerrank.com/challenges/harry-potter-and-wands/problem?isFullScreen=true)
```
SELECT w.id, wp.age, w.coins_needed, w.power
FROM Wands AS w INNER JOIN Wands_Property AS wp
ON w.code = wp.code AND wp.is_evil = 0
WHERE w.coins_needed = (SELECT MIN( coins_needed )
                                         FROM Wands 
                                         WHERE code = w.code and power = w.power )
ORDER BY w.power DESC, wp.age DESC;
```




# Sources
[Blog](https://www.w3schools.com/MySQL/)
[Video](https://youtu.be/aZnwpMON0NA?si=xsxKUiesnuLZX7gC)
