# Type of Triangle
  
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

- Equilateral: It's a triangle with ***3*** sides of equal length.
- Isosceles: It's a triangle with ***2** sides of equal length.
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
    
**Ans**

	SELECT 
 	CASE 
        WHEN (A + C <= B)  OR  (A + B <= C) OR (B + C <= A) THEN 'Not A Triangle'
        WHEN (A = B) AND (B = C) THEN 'Equilateral'
        WHEN (A =B) OR (C = A) OR (B = C) THEN 'Isosceles'
        ELSE 'Scalene'
	END 
	FROM TRIANGLES;
    
# The PADS
  
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
    
**Ans**

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
        END, 
      '.') AS summary
    FROM OCCUPATIONS 
    GROUP BY OCCUPATION
    ORDER BY COUNT(OCCUPATION) ASC, OCCUPATION ASC;
    
# Binary Tree Nodes
  
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

	SELECT
	    N,
	    CASE
	        WHEN P IS NULL THEN 'Root'
	        WHEN N IN (SELECT P FROM BST) THEN 'Inner'
	        ELSE 'Leaf'
	    END
	FROM BST
	ORDER  BY N;

# New Companies
No desc just straight answer(im lazy to add it lul)

**Ans**

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
 
# Occupations
No desc just straight answer(im lazy to add it lul)

**Ans**

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
	SELECT Doctor, Professor, Singer, Actor
	FROM Pivoted
	ORDER BY RowNum;


