# Revising the Select Query I 
  
Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.

The CITY table is described as follows:  

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

    SELECT
      *
    FROM CITY
    WHERE COUNTRYCODE = "USA" AND POPULATION > 100000;

# Revising the Select Query II 

Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.

The CITY table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

    SELECT 
      NAME 
    FROM CITY
    WHERE COUNTRYCODE = "USA" AND POPULATION > 120000;
    
# Select All

Query all columns (attributes) for every row in the CITY table.

The CITY table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

    SELECT 
      * 
    FROM CITY;

# Select By ID

Query all columns for a city in CITY with the ID 1661.

The CITY table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

    SELECT 
      * 
    FROM CITY 
    WHERE ID = 1661;
    
# Japanese Cities' Attributes

Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.

The CITY table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

    SELECT
      * 
    FROM CITY
    WHERE COUNTRYCODE = "JPN";
    
# Japanese Cities' Names

Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.

The CITY table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

    SELECT
      NAME
    FROM CITY
    WHERE COUNTRYCODE = "JPN";
       
# Weather Observation Station 1

Query a list of CITY and STATE from the STATION table.

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT
      CITY, 
      STATE
    FROM STATION;
      
# Weather Observation Station 3

Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT
      DISTINCT CITY
    FROM STATION
    WHERE ID % 2 = 0;
         
# Weather Observation Station 4

Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

For example, if there are three records in the table with CITY values 'New York', 'New York', 'Bengalaru', there are 2 different city names: 'New York' and 'Bengalaru'. The query returns ***1***, because
***total number of records - number of unique city names = 3 - 2 = 1.***

    SELECT 
      (COUNT(CITY) - COUNT(DISTINCT CITY))
    FROM STATION;
             
# Weather Observation Station 5

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

**Sample Input**
For example, CITY has four entries: DEF, ABC, PQRS and WXY.

**Sample Output**
    ABC 3
    PQRS 4

**Explanation**
When ordered alphabetically, the CITY names are listed as ABC, DEF, PQRS, and WXY, with lengths ***3***,  ***3***, ***4***, and ***3***. The longest name is PQRS, but there are ***3*** options for shortest named city. Choose ABC, because it comes first alphabetically.

**Note**
You can write two separate queries to get the desired output. It need not be a single query.

    SELECT 
      DISTINCT CITY, 
      LENGTH(CITY) AS CITY_LENGTH
    FROM STATION
    WHERE LENGTH(CITY) = (SELECT MIN(LENGTH(CITY)) FROM STATION)
    ORDER BY CITY
    LIMIT 1;

    SELECT 
      DISTINCT CITY, 
      LENGTH(CITY) AS CITY_LENGTH
    FROM STATION
    WHERE LENGTH(CITY) = (SELECT MAX(LENGTH(CITY)) FROM STATION)
    ORDER BY CITY
    LIMIT 1;
             
# Weather Observation Station 6

Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

**Input Format**

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT 
      DISTINCT CITY 
    FROM STATION
    WHERE CITY LIKE "A%" 
      OR CITY LIKE "E%" 
      OR CITY LIKE "I%" 
      OR CITY LIKE "O%" 
      OR CITY LIKE "U%";
            
# Weather Observation Station 7

Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

**Input Format**

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT 
      DISTINCT CITY 
    FROM STATION
    WHERE CITY LIKE "%a" 
      OR CITY LIKE "%e" 
      OR CITY LIKE "%i" 
      OR CITY LIKE "%o" 
      OR CITY LIKE "%u";
                  
# Weather Observation Station 8

Query the list of CITY names from STATION which have vowels (i.e., a, e, i, o, and u) as both their first and last characters. Your result cannot contain duplicates.

**Input Format**

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT 
      DISTINCT city 
    FROM station 
    WHERE (city LIKE 'A%' 
        OR city LIKE 'E%' 
        OR city LIKE 'I%' 
        OR city LIKE 'O%' 
        OR city LIKE 'U%')
    AND (city LIKE '%a'
      OR city LIKE '%e' 
      OR city LIKE '%i' 
      OR city LIKE '%o' 
      OR city LIKE '%u');
                        
# Weather Observation Station 9

Query the list of CITY names from STATION that do not start with vowels. Your result cannot contain duplicates.

**Input Format**

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT 
      DISTINCT city
    FROM station
    WHERE city NOT LIKE 'A%' 
      AND city NOT LIKE 'E%' 
      AND city NOT LIKE 'I%' 
      AND city NOT LIKE 'O%' 
      AND city NOT LIKE 'U%';
      
# Weather Observation Station 10

Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.

**Input Format**

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT 
      DISTINCT city
    FROM station
    WHERE city NOT LIKE '%a' 
      AND city NOT LIKE '%e' 
      AND city NOT LIKE '%i' 
      AND city NOT LIKE '%u' 
      AND city NOT LIKE '%o' ;
      
# Weather Observation Station 11

Query the list of CITY names from STATION that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

**Input Format**

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT 
      DISTINCT city
    FROM station
    WHERE (city NOT LIKE 'A%' 
      AND city NOT LIKE 'E%' 
      AND city NOT LIKE 'I%' 
      AND city NOT LIKE 'O%' 
      AND city NOT LIKE 'U%')
    OR (city NOT LIKE '%a' 
    AND city NOT LIKE '%e' 
    AND city NOT LIKE '%i' 
    AND city NOT LIKE '%o' 
    AND city NOT LIKE '%u');
    
# Weather Observation Station 12

Query the list of CITY names from STATION that do not start with vowels and do not end with vowels. Your result cannot contain duplicates.

**Input Format**

The STATION table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/9336/1449345840-5f0a551030-Station.jpg)

where LAT_N is the northern latitude and LONG_W is the western longitude.

    SELECT 
      DISTINCT city
    FROM station
    WHERE (city NOT LIKE 'A%' 
      AND city NOT LIKE 'E%' 
      AND city NOT LIKE 'I%' 
      AND city NOT LIKE 'O%' 
      AND city NOT LIKE 'U%')
    AND (city NOT LIKE '%a' 
      AND city NOT LIKE '%e' 
      AND city NOT LIKE '%i' 
      AND city NOT LIKE '%o' 
      AND city NOT LIKE '%u');
      
# Higher Than 75 Marks

Query the Name of any student in STUDENTS who scored higher than ***75*** Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.

**Input Format**

The STUDENTS table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/12896/1443815243-94b941f556-1.png)

The Name column only contains uppercase (A-Z) and lowercase (a-z) letters.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12896/1443815209-cf4b260993-2.png)

**Sample Output**
    Ashley
    Julia
    Belvet

**Explanation**
Only Ashley, Julia, and Belvet have Marks > ***75***. If you look at the last three characters of each of their names, there are no duplicates and 'ley' < 'lia' < 'vet'.

    SELECT 
      NAME
    FROM STUDENTS
    WHERE MARKS > 75
    ORDER BY RIGHT(NAME, 3), ID ASC;
    
# Employee Names

Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.

**Input Format**

The Employee table containing employee data for a company is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is their monthly salary.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458558202-9a8721e44b-ScreenShot2016-03-21at4.32.59PM.png)

**Sample Output**
    Angela
    Bonnie
    Frank
    Joe
    Kimberly
    Lisa
    Michael
    Patrick
    Rose
    Todd

    SELECT
      NAME
    FROM EMPLOYEE
    ORDER BY NAME ASC;
    
# Employee Salaries

Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than ***$2000*** per month who have been employees for less than ***10*** months. Sort your result by ascending employee_id.

**Input Format**

The Employee table containing employee data for a company is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

where employee_id is an employee's ID number, name is their name, months is the total number of months they've been working for the company, and salary is the their monthly salary.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/19630/1458558612-af3da3ceb7-ScreenShot2016-03-21at4.32.59PM.png)

**Sample Output**
    Angela
    Michael
    Todd
    Joe

**Explanation**

Angela has been an employee for ***1*** month and earns ***$3443*** per month.

Michael has been an employee for ***6*** months and earns ***$2017*** per month.

Todd has been an employee for ***5*** months and earns ***$3396*** per month.

Joe has been an employee for ***9*** months and earns ***$3573*** per month.

We order our output by ascending employee_id.

    SELECT 
      NAME
    FROM EMPLOYEE
    WHERE SALARY > 2000 AND MONTHS < 10;

