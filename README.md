# HackerankPracticefirst20Queries


#2. Query the names of all American cities in CITY with populations larger than 120000. The CountryCode for America is USA.
/*
Enter your query here.
Please append a semicolon ";" at the end of the query and enter your query in a single line to avoid error.
*/ select name from city 
where
CountryCode = 'USA' and 
population > 120000;

#3.Query all columns (attributes) for every row in the CITY table.
/*
Enter your query here.
Please append a semicolon ";" at the end of the query and enter your query in a single line to avoid error.
*/ select * from city;

#4.Query all columns for a city in CITY with the ID 1661.
/*
Enter your query here.
Please append a semicolon ";" at the end of the query and enter your query in a single line to avoid error.
*/ select * from city where id = 1661

#5.Let  be the number of CITY entries in STATION, and let  be the number of distinct CITY names in STATION; query the value of  from STATION. In other words, find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

Input Format
/*
Enter your query here.
Please append a semicolon ";" at the end of the query and enter your query in a single line to avoid error.
*/ select count(city)-count(distinct(city)) from station;

#6.Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

/*
Enter your query here.
Please append a semicolon ";" at the end of the query and enter your query in a single line to avoid error.
*/ DECLARE @V1 VARCHAR(MAX)

DECLARE @V2 VARCHAR(MAX)

DECLARE @V3 VARCHAR(MAX)

DECLARE @V4 VARCHAR(MAX)

SET @V1 = (SELECT MIN(LEN(CITY)) FROM STATION);

SET @V2 = (SELECT TOP 1 CITY FROM STATION WHERE LEN(CITY) = @V1 ORDER BY CITY );

SET @V3 = (SELECT MAX(LEN(CITY)) FROM STATION);

SET @V4 = (SELECT TOP 1 CITY FROM STATION WHERE LEN(CITY) = @V3 ORDER BY CITY );

SELECT @V2,@V1; SELECT @V4,@V3;


#Alternate solutions
select top 1 CITY,min(len(CITY)) len from STATION group by CITY order by len asc; 
select top 1 CITY,max(len(CITY)) len from STATION group by CITY order by len desc;


#7.Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. 
Your result cannot contain duplicates.
/*
Enter your query here.
Please append a semicolon ";" at the end of the query and enter your query in a single line to avoid error.
*/select distinct(city) from station where
substring(city,1,1) in ('a', 'e', 'i', 'o', 'u')
order by city;



#8.Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.
SELECT DISTINCT city FROM   station 
WHERE  city  LIKE lower('%A') 
or  city  LIKE lower('%E') 
or city  LIKE lower('%I') 
or city  LIKE lower('%O') 
or city  LIKE lower('%U');


#9.Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) 
as both their first and last characters. Your result cannot contain duplicates.

select distinct city from station 
where left(city,1) in ('a','e','i','o','u') 
and right(city, 1) in ('a','e','i','o','u')​;


#10.Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.
select distinct city from station 
where left(city,1) not in ('a','e','i','o','u');

#11.Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. 
Your result cannot contain duplicates.
select distinct city from station 
where left(city,1) not in ('a','e','i','o','u') 
or right(city, 1) not in ('a','e','i','o','u')
order by city;


#12. Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. 
Your result cannot contain duplicates.
select distinct city from station 
where left(city,1) not in ('a','e','i','o','u') 
and right(city, 1) not in ('a','e','i','o','u')
order by city;

#13.Query the Name of any student in STUDENTS who scored higher than  Marks. 
Order your output by the last three characters of each name. If two or more students 
both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

select name from students
where marks >75
order by right(name,3) asc, id asc;

#14.Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.
select name from employee
order by name;

#15.Write a query that prints a list of employee names (i.e.: the name attribute) 
for employees in Employee having a salary greater than 2000 per month who have been employees 
for less than 10 months. Sort your result by ascending employee_id.
select name from employee
where salary>2000 and months<10
order by employee_id;

#16.Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than . 
Round your answer to 4 decimal places.
'N4' is equvivalent to 4 places as .1234 similarly 'N3'is .123
/*Important to round up values*/
select format(LONG_W,'N4') from station where lat_n = 
(select max(lat_n) from station where lat_n < 137.2345137);

#17.Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.7780. Round your answer to 4 decimal places.
select format(lat_n,'N4') from station where lat_n = 
(select min(lat_n) from station where lat_n >38.7780);

#18.Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780. 
Round your answer to 4 decimal places.
select format(LONG_W,'N4') from station where lat_n = 
(select min(lat_n) from station where lat_n >38.7780);

#19.ConsiderP1(a,b)  andP2(c,d)  to be two points on a 2D plane.

 a happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
 b happens to equal the minimum value in Western Longitude (LONG_W in STATION).
 c happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
 d happens to equal the maximum value in Western Longitude (LONG_W in STATION).
Query the Manhattan Distance between points  and  and round it to a scale of  decimal places.

SELECT FORMAT(ABS(MIN(LAT_N)-MAX(LAT_N))+ABS(MIN(LONG_W)-MAX(LONG_W)),'N4') FROM STATION;


#20. Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. 
Output one of the following statements for each record in the table:

Equilateral: It's a triangle with  sides of equal length.
Isosceles: It's a triangle with  sides of equal length.
Scalene: It's a triangle with  sides of differing lengths.
Not A Triangle: The given values of A, B, and C don't form a triangle.


SELECT CASE WHEN A + B <= C OR A + C <= B OR B + C <= A THEN 'Not A Triangle'
            WHEN A = B AND B = C THEN 'Equilateral'
            WHEN A = B OR A = C OR B = C THEN 'Isosceles'
            ELSE 'Scalene'
        END
FROM TRIANGLES


