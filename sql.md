<!--Revising the Select Query I-- >

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






# Aggregation

# Query a count of the number of cities in CITY having a Population larger than 100000 .

SELECT
    COUNT(NAME)
FROM
    City
WHERE
    Population >= 100000


# Query the total population of all cities in CITY where District is California.

SELECT
    SUM(population)
FROM
    City
WHERE   
    District = 'California'

# Query the AVG population of all cities in CITY where District is California.

SELECT
    AVG(population)
FROM
    City
WHERE   
    District = 'California'


# Query the average population for all cities in CITY, rounded down to the nearest integer.

SELECT
    ROUND(AVG(Population))
FROM    
    City


# Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.

SELECT
    SUM(population)
FROM
    City
WHERE
    COUNTRYCODE = 'JPN'


# Query the difference between the maximum and minimum populations in CITY.

SELECT
    MAX(population) - MIN(population)
FROM
    City


# Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's  key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeros removed), and the actual average salary.
Write a query calculating the amount of error (i.e.:  average monthly salaries), and round it up to the next integer.

SELECT
    CEIL(AVG(Salary) - AVG(Replace(Salary, 0, '')))
FROM
    Employees




# We define an employee's total earnings to be their monthly  worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as  space-separated integers.

SELECT
    Salary * Months AS EARNINGS,
    COUNT(*)
FROM
    Employee
GROUP BY
    EARNINGS
ORDER BY    
    EARNINGS DESC 
LIMIT 
    1


# Query the following two values from the STATION table:

SELECT
    ROUND(SUM(LAT_N),2),
    ROUND(SUM(LONG_W),2)
FROM
    STATION

# Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than  and less than . Truncate your answer to  decimal places. WOB13

SELECT
    ROUND(SUM(LAT_N),4)
FROM
    STATION
WHERE
    LAT_N > 38.7850 AND LAT_N < 137.2345

# Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than . Truncate your answer to  decimal places.

SELECT
    ROUND(MAX(LAT_N),4)
FROM
    STATION
WHERE
    LAT_N < 137.2345


# Query the smallest Northern Latitude (LAT_N) from STATION that is greater than . Round your answer to  decimal places.


SELECT
    ROUND(LAT_N,4)
FROM
    Station
WHERE
    LAT_N > 38.7780
ORDER BY 
    LAT_N ASC
LIMIT 1


# Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than . Round your answer to  decimal places.

SELECT 
    ROUND(LONG_W, 4)
FROM 
    Station
WHERE
    LAT_N > 38.7780
ORDER BY    
    LAT_N 
LIMIT 1
    

# Consider  and  to be two points on a 2D plane.

 happens to equal the minimum value in Northern Latitude (LAT_N in STATION).
 happens to equal the minimum value in Western Longitude (LONG_W in STATION).
 happens to equal the maximum value in Northern Latitude (LAT_N in STATION).
 happens to equal the maximum value in Western Longitude (LONG_W in STATION).
Query the Manhattan Distance between points  and  and round it to a scale of  decimal places.


SELECT
    ROUND((MAX(LAT_N)-MIN(LAT_N)) + ((MAX(LONG_W) - MIN(LONG_W))),4)   
FROM
    STATION


# Consider  and  to be two points on a 2D plane where  are the respective minimum and maximum values of Northern Latitude (LAT_N) and  are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.Query the Euclidean Distance between points  and  and format your answer to display  decimal digits.
SELECT
    ROUND(SQRT(((MAX(LAT_N) - MIN(LAT_N)) *  (MAX(LAT_N) - MIN(LAT_N))) +  
    ((MAX(LONG_W) - MIN(LONG_W)) * (MAX(LONG_W) - MIN(LONG_W)))),4)
FROM   
    STATION




# A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to  decimal places.
SELECT ROUND(LAT_N,4) FROM 

(SELECT
    ROW_NUMBER()
    OVER (ORDER BY LAT_N) AS RNK,
    LAT_N
FROM
    STATION ) AS A 

WHERE RNK = (
    SELECT
        ROUND(COUNT(*)/2)
    FROM
        STATION
)

## BASIC JOINS

# Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

SELECT
    SUM(CITY.POPULATION)
FROM 
    CITY
JOIN 
    COUNTRY 
ON
    CITY.CountryCode =  COUNTRY.Code
WHERE
    CONTINENT  = 'Asia'

# Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

SELECT
    City.Name
FROM
    City
JOIN 
    Country
ON
   CITY.CountryCode =  COUNTRY.Code 
WHERE
    CONTINENT = 'Africa'


## Average Population of Each Continent

SELECT
    COUNTRY.Continent,
    floor(avg(CITY.population))
FROM
    City
JOIN 
    Country
ON  
    CITY.CountryCode = COUNTRY.Code
GROUP BY
    COUNTRY.Continent




## You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.

SELECT
    IF(Grade<8, Null, Name), Grade , Marks
FROM
    Students S
JOIN
    Grades G
WHERE
    S.Marks BETWEEN G.MIN_MARK AND G.MAX_MARK
ORDER BY
    Grade DESC,
    NAME ASC

## Top Competitors

SELECT H.HACKER_ID, H.NAME
FROM HACKERS H
INNER JOIN SUBMISSIONS S
ON H.HACKER_ID = S.HACKER_ID
INNER JOIN CHALLENGES C
ON S.CHALLENGE_ID = C.CHALLENGE_ID
INNER JOIN DIFFICULTY D
ON C.DIFFICULTY_LEVEL = D.DIFFICULTY_LEVEL
WHERE S.SCORE = D.SCORE
GROUP BY H.HACKER_ID, H.NAME
HAVING COUNT(S.HACKER_ID) > 1
ORDER BY COUNT(S.HACKER_ID) DESC, S.HACKER_ID ASC;

## Ollivander's Inventory
/
SELECT W.ID, P.AGE, W.COINS_NEEDED, W.POWER 
FROM WANDS AS W
JOIN WANDS_PROPERTY AS P
ON (W.CODE = P.CODE) 
WHERE P.IS_EVIL = 0 AND W.COINS_NEEDED = (SELECT MIN(COINS_NEEDED) 
                                          FROM WANDS AS X
                                          JOIN WANDS_PROPERTY AS Y 
                                          ON (X.CODE = Y.CODE) 
                                          WHERE X.POWER = W.POWER AND Y.AGE = P.AGE) 
ORDER BY W.POWER DESC, P.AGE DESC;