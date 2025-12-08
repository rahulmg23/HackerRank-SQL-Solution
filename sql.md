
<!--Revising the Select Query I-->
SELECT
    *
FROM    
    City
WHERE   
    Population > 120000
AND 
    CountryCode = 'USA'



<!--Revising the Select Query II-->
SELECT
    name
FROM    
    City
WHERE   
    Population > 120000
AND 
    CountryCode = 'USA'


<!-- Select All -->
SELECT
    *
FROM    
    City


<!-- Select All By city id is 166` -->
SELECT
    *
FROM    
    City
WHERE
    ID = 1661


<!-- Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN. -->
SELECT
    *
FROM 
    City
WHERE   
    COUNTRYCODE = 'JPN'


<!-- Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.  -->
SELECT
    name
FROM    
    City
WHERE   
    COUNTRYCODE = 'JPN'


<!-- Query a list of CITY and STATE from the STATION table. -->
SELECT
    City,
    State
FROM    
    Station

<!-- Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer. -->
SELECT  
   Distinct City
FROM    
    Station
WHERE
    id%2 = 0 


<!-- Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table. -->
SELECT 
    COUNT(City) - COUNT(DISTINCT CITY)
FROM    
    Station

<!-- Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically. -->

(SELECT
    City,
    char_length(city)
FROM
    Station
ORDER BY    
    char_length(city) asc,
    City
LIMIT 1)
UNION ALL
(
    SELECT
    City,
    char_length(city)
FROM
    Station
ORDER BY    
    char_length(city) DESC,
    City
LIMIT 1
)


<!-- Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.-->

SELECT
    DISTINCT City
FROM    
    Station
WHERE
    City REGEXP '^[aeiou]'


<!-- Query the list of CITY names ending with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.-->

SELECT
    DISTINCT City
FROM    
    Station
WHERE
    City REGEXP '[aeiou]$'



<!-- Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates. -->
SELECT  
    DISTINCT City 
FROM 
    Station
WHERE   
    City REGEXP '^[aeiou].*[aeiou]$'

<!-- Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates. -->
SELECT
    Distinct City
FROM    
    Station
WHERE
    City NOT REGEXP '^[aeiou]'

<!-- Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates. -->
SELECT
    DISTINCT City
FROM
    Station
WHERE
    City NOT REGEXP '[aeiou]$'


<!-- Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates. -->
SELECT
    DISTINCT City
FROM
    Station
WHERE
    City not REGEXP '^[aeiou].*[aeiou]$'


<!--  Query the Name of any student in STUDENTS who scored higher than  Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID. -->
SELECT
    Name
FROM
    Students
WHERE 
    Marks > 75
ORDER BY
    SUBSTR(name,-3) , id asc
    
<!-- Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order. -->
SELECT
    Name
FROM
    Employee
ORDER BY
    Name asc
    

<!-- Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than  per month who have been employees for less than  months. Sort your result by ascending employee_id. -->
SELECT
    NAME
FROM 
    EMPLOYEE
WHERE 
    SALARY > 2000 AND MONTHS < 10 
ORDER BY
     EMPLOYEE_ID;
