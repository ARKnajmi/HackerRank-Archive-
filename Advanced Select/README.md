### 📌 **Type of Triangle**
  
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

- Equilateral: It's a triangle with ***3*** sides of equal length.
- Isosceles: It's a triangle with ***2*** sides of equal length.
- Scalene: It's a triangle with ***3*** sides of differing lengths.
- Not A Triangle: The given values of A, B, and C don't form a triangle.

**Input Format**

The TRIANGLES table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/12887/1443815629-ac2a843fb7-1.png)

Each row in the table denotes the lengths of each of a triangle's three sides.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12887/1443815827-cbfc1ca12b-2.png)

**Sample Output**

    Isosceles
    Equilateral
    Scalene
    Not A Triangle
    
**Answer**
```sql
SELECT
 CASE 
  WHEN (A + C <= B)  OR  (A + B <= C) OR (B + C <= A) THEN 'Not A Triangle'
  WHEN (A = B) AND (B = C) THEN 'Equilateral'
  WHEN (A =B) OR (C = A) OR (B = C) THEN 'Isosceles'
  ELSE 'Scalene'
 END
FROM TRIANGLES;
```

### 📌 **The PADS**
  
Generate the following two result sets:

1. Query an alphabetically ordered list of all names in **OCCUPATIONS**, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
   
2. Query the number of ocurrences of each occupation in **OCCUPATIONS**. Sort the occurrences in ascending order, and output them in the following format:

       There are a total of [occupation_count] [occupation]s.
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

**Note:** There will be at least two entries in the table for each type of occupation.

**Input Format**

The  **OCCUPATIONS** table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png)

Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

**Sample Input**

An OCCUPATIONS table that contains the following records:

![img](https://s3.amazonaws.com/hr-challenge-images/12889/1443816608-0b4d01d157-2.png)

**Sample Output**

    Ashely(P)
    Christeen(P)
    Jane(A)
    Jenny(D)
    Julia(A)
    Ketty(P)
    Maria(A)
    Meera(S)
    Priya(S)
    Samantha(D)
    There are a total of 2 doctors.
    There are a total of 2 singers.
    There are a total of 3 actors.
    There are a total of 3 professors.
    
**Answer**
```sql
SELECT
 CONCAT(NAME,
 CASE
  WHEN OCCUPATION LIKE "Doc%" THEN "(D)"
  WHEN OCCUPATION LIKE "Act%" THEN "(A)"
  WHEN OCCUPATION LIKE "Sing%" THEN "(S)"
  WHEN OCCUPATION LIKE "Prof%" THEN "(P)"
 END
)
FROM OCCUPATIONS
ORDER BY NAME ASC;

SELECT
 CONCAT('There are a total of ', COUNT(OCCUPATION), ' ', 
 CASE 
  WHEN LOWER(OCCUPATION) LIKE '%s' THEN LOWER(OCCUPATION)
  ELSE CONCAT(LOWER(OCCUPATION), 's')
 END, '.') AS summary
FROM OCCUPATIONS 
GROUP BY OCCUPATION
ORDER BY COUNT(OCCUPATION) ASC, OCCUPATION ASC;
```
    
### 📌 **Binary Tree Nodes**
  
You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png)

Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:

- Root: If node is root node.
- Leaf: If node is leaf node.
- Inner: If node is neither root nor leaf node.
  
**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443818467-30644673f6-2.png)

**Sample Output**

	1 Leaf
	2 Inner
	3 Leaf
	5 Root
	6 Leaf
	8 Inner
	9 Leaf
    
**Explanation**
The Binary Tree below illustrates the sample:

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443773633-f9e6fd314e-simply_sql_bst.png)
```sql
SELECT
 N,
 CASE
  WHEN P IS NULL THEN 'Root'
  WHEN N IN (SELECT P FROM BST) THEN 'Inner'
  ELSE 'Leaf'
 END
FROM BST
ORDER  BY N;
```
### 📌 **New Companies**
Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy: 
![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png)

Given the table schemas below, write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

**Note:**
* The tables may contain duplicate records.
* The company_code is string, so the sorting should not be **numeric**. For example, if the company_codes are C_1, C_2, and C_10, then the ascending company_codes will be C_1, C_10, and C_2.
___

**Input Format**
The following tables contain company data:

* Company: The company_code is the code of the company and founder is the founder of the company.
   
	![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458531125-deb0a57ae1-ScreenShot2016-03-21at8.50.04AM.png)

* Lead_Manager: The lead_manager_code is the code of the lead manager, and the company_code is the code of the working company.
   
	![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458534960-2c6d764e3c-ScreenShot2016-03-21at8.50.12AM.png)

* Senior_Manager: The senior_manager_code is the code of the senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.
  
	![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458534973-6548194998-ScreenShot2016-03-21at8.50.21AM.png)

* Manager: The manager_code is the code of the manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.
   
	![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458534988-7fc0af46ce-ScreenShot2016-03-21at8.50.29AM.png)

* Employee: The employee_code is the code of the employee, the manager_code is the code of its manager, the senior_manager_code is the code of its senior manager, the lead_manager_code is the code of its lead manager, and the company_code is the code of the working company.
   
	![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535002-d47f63cbb4-ScreenShot2016-03-21at8.50.41AM.png)

___

**Sample Input**
Company Table:

![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535049-2a207c44b3-ScreenShot2016-03-21at8.50.52AM.png)

Lead_Manager Table:

![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535073-919107f639-ScreenShot2016-03-21at8.51.03AM.png)

Senior_Manager Table:

![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535111-b1c48335b3-ScreenShot2016-03-21at8.51.15AM.png)

Manager Table:

![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535122-888f4bf340-ScreenShot2016-03-21at8.51.26AM.png)

Employee Table: 

![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535134-878767e0d9-ScreenShot2016-03-21at8.51.52AM.png)


**Sample Output**

		C1 Monika 1 2 1 2
		C2 Samantha 1 1 2 2

**Explanation**

In company C1, the only lead manager is LM1. There are two senior managers, SM1 and SM2, under LM1. There is one manager, M1, under senior manager SM1. There are two employees, E1 and E2, under manager M1.

In company C2, the only lead manager is LM2. There is one senior manager, SM3, under LM2. There are two managers, M2 and M3, under senior manager SM3. There is one employee, E3, under manager M2, and another employee, E4, under manager, M3.

**Answer**
```sql
SELECT 
 t1.company_code,
 t1.founder,
 COUNT(DISTINCT t2.lead_manager_code) AS lead_manager_count,
 COUNT(DISTINCT t3.senior_manager_code) AS senior_manager_count,
 COUNT(DISTINCT t4.manager_code) AS manager_count,
 COUNT(DISTINCT t5.employee_code) AS employee_count
FROM Company t1
INNER JOIN Lead_Manager t2 
 ON t1.company_code = t2.company_code 
INNER JOIN Senior_Manager t3 
 ON t2.company_code = t3.company_code 
INNER JOIN Manager t4 
 ON t3.company_code = t4.company_code 
INNER JOIN Employee t5 
 ON t4.company_code = t5.company_code
GROUP BY t1.company_code, t1.founder;
```
 
### 📌 **Occupations**
Pivot the Occupation column in **OCCUPATIONS** so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

**Note:** Print **NULL** when there are no more names corresponding to an occupation.

**Input Format**

The **OCCUPATIONS** table is described as follows:
![img](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png)

Occupation will only contain one of the following values: **Doctor, Professor, Singer** or **Actor.**

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12890/1443817648-1b2b8add45-2.png)]

**Sample Output**

			Jenny    Ashley     Meera  Jane
			Samantha Christeen  Priya  Julia
			NULL     Ketty      NULL   Maria

**Answer**
```sql
WITH makeRowNum AS (
 SELECT
  NAME,
  OCCUPATION,
  ROW_NUMBER() OVER (PARTITION BY OCCUPATION ORDER BY NAME) AS RowNum
 FROM OCCUPATIONS
),
Pivoted AS (
 SELECT
  MAX(CASE 
   WHEN OCCUPATION = 'Doctor' THEN NAME 
  END) AS Doctor,
  MAX(CASE
   WHEN OCCUPATION = 'Professor' THEN NAME 
  END) AS Professor,
  MAX(CASE 
   WHEN OCCUPATION = 'Singer' THEN NAME 
  END) AS Singer,
  MAX(CASE 
   WHEN OCCUPATION = 'Actor' THEN NAME 
  END) AS Actor,
  RowNum
FROM makeRowNum
GROUP BY RowNum
)
SELECT
 Doctor,
 Professor,
 Singer,
 Actor
FROM Pivoted
ORDER BY RowNum;
```



