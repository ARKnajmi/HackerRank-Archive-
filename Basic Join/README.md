# 📌 **Population Census** 
  
Given the **CITY** and **COUNTRY** tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

Input Format

The **CITY** and **COUNTRY** tables are described as follows:  

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

![img](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)

**Answer**

```sql
SELECT
 SUM(CITY.POPULATION)
FROM CITY
INNER JOIN COUNTRY
 ON COUNTRYCODE = CODE
WHERE CONTINENT = "Asia";
```

# 📌 **African Cities** 
  
Given the **CITY** and **COUNTRY** tables, query the names of all cities where the CONTINENT is 'Africa'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

Input Format

The **CITY** and **COUNTRY** tables are described as follows:  

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

![img](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)

**Answer**

```sql
SELECT
 CITY.NAME
FROM CITY
INNER JOIN COUNTRY
 ON COUNTRYCODE = CODE
WHERE CONTINENT = "Africa";
```

# 📌 **Average Population of Each Continent** 
  
Given the **CITY** and **COUNTRY** tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer. 

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

Input Format

The **CITY** and **COUNTRY** tables are described as follows:  

![img](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

![img](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)

**Answer**

```sql
SELECT
 CONTINENT,
 FLOOR(AVG(CITY.POPULATION))
FROM CITY
INNER JOIN COUNTRY
 ON COUNTRYCODE = CODE
GROUP BY CONTINENT;
```

# 📌 **The Report** 
  
You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.

![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818166-a5c852caa0-1.png)

Grades contains the following data:

![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818137-69b76d805c-2.png)

Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Write a query to help Eve.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818093-b79f376ec1-3.png)

**Sample Output**

    Maria 10 99
    Jane 9 81
    Julia 9 88 
    Scarlet 8 78
    NULL 7 63
    NULL 7 68

**Note**

Print "NULL"  as the name if the grade is less than 8.

**Explanation**

Consider the following table with the grades assigned to the students:

![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818026-0b3af8db30-4.png)

So, the following students got 8, 9 or 10 grades:

* Maria (grade 10)
* Jane (grade 9)
* Julia (grade 9)
* Scarlet (grade 8)

**Answer**

```sql
SELECT
 IF(GRADE >= 8, NAME, NULL),
 GRADES.GRADE, 
 STUDENTS.MARKS
FROM STUDENTS
JOIN GRADES
WHERE MARKS BETWEEN MIN_MARK AND MAX_MARK
ORDER BY GRADE DESC, NAME;
```

# 📌 **Top Competitors** 
  
Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.
___

**Input Format**

The following tables contain contest data:

* Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.

![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458526776-67667350b4-ScreenShot2016-03-21at7.45.59AM.png)

* Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level.

![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458526915-57eb75d9a2-ScreenShot2016-03-21at7.46.09AM.png)

* Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge. 

![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527032-f9ca650442-ScreenShot2016-03-21at7.46.17AM.png)

* Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.

![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527077-298f8e922a-ScreenShot2016-03-21at7.46.29AM.png)
___

**Sample Input**

Hackers Table: 

![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527241-6922b4ad87-ScreenShot2016-03-21at7.47.02AM.png)

Difficulty Table:

![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527265-7ad6852a13-ScreenShot2016-03-21at7.46.50AM.png)

Challenges Table:

![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527285-01e95eb6ec-ScreenShot2016-03-21at7.46.40AM.png)

Submissions Table:

![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527812-479a74b99f-ScreenShot2016-03-21at8.06.05AM.png)


**Sample Output**

    90411 Joe

**Explanation**

Hacker 86870 got a score of 30 for challenge 71055 with a difficulty level of 2, so 86870 earned a full score for this challenge.

Hacker 90411 got a score of 30 for challenge 71055 with a difficulty level of 2, so 90411 earned a full score for this challenge.

Hacker 90411 got a score of 100 for challenge 66730 with a difficulty level of 6, so 90411 earned a full score for this challenge.

Only hacker 90411 managed to earn a full score for more than one challenge, so we print the their hacker_id and name as *2* space-separated values.

**Answer**

```sql
SELECT
 H.HACKER_ID,
 H.NAME
FROM HACKERS H
JOIN SUBMISSIONS S
 ON H.HACKER_ID = S.HACKER_ID
JOIN CHALLENGES C
 ON S.CHALLENGE_ID = C.CHALLENGE_ID
JOIN DIFFICULTY D
 ON C.DIFFICULTY_LEVEL = D.DIFFICULTY_LEVEL
WHERE S.SCORE = D.SCORE
GROUP BY H.HACKER_ID, H.NAME
HAVING COUNT(S.HACKER_ID) > 1
ORDER BY COUNT(S.HACKER_ID) DESC, S.HACKER_ID ASC;
```

# 📌 **Ollivander's Inventory** 
  
Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.

Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power and age. Write a query to print the id, age, coins_needed, and power of the wands that Ron's interested in, sorted in order of descending power. If more than one wand has same power, sort the result in order of descending age.

**Input Format**

The following tables contain data on the wands in Ollivander's inventory:

* Wands: The id is the id of the wand, code is the code of the wand, coins_needed is the total number of gold galleons needed to buy the wand, and power denotes the quality of the wand (the higher the power, the better the wand is).

  ![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458538092-b2a8163a74-ScreenShot2016-03-08at12.13.39AM.png)
  
*Wands_Property: The code is the code of the wand, age is the age of the wand, and is_evil denotes whether the wand is good for the dark arts. If the value of is_evil is 0, it means that the wand is not evil. The mapping between code and age is one-one, meaning that if there are two pairs, *(code1, age1)* and *(code2, age2)*, then *code1 != code2* and *age1 != age2*.

  ![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458538221-18c4092b7d-ScreenShot2016-03-08at12.13.53AM.png)
___

**Sample Input**

Wands Table: 

![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458538559-51bf29644e-ScreenShot2016-03-21at10.34.41AM.png)

Wands_Property Table:

![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458538583-fd514566f9-ScreenShot2016-03-21at10.34.28AM.png)

**Sample Output**

    9 45 1647 10
    12 17 9897 10
    1 20 3688 8
    15 40 6018 7
    19 20 7651 6
    11 40 7587 5
    10 20 504 5
    18 40 3312 3
    20 17 5689 3
    5 45 6020 2
    14 40 5408 1

**Explanation**

The data for wands of age 45 (code 1):

![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458539700-2f319702ab-ScreenShot2016-03-21at11.23.06AM.png)

* The minimum number of galleons needed for *wand(age = 45, power = 2) = 6020*
* The minimum number of galleons needed for *wand(age = 45, power = 10) = 1647*
  
The data for wands of age 40 (code 2):

![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458539909-ab79f7ff95-ScreenShot2016-03-21at11.23.14AM.png)

* The minimum number of galleons needed for *wand(age = 40, power = 1) = 5408*
* The minimum number of galleons needed for *wand(age = 40, power = 3) = 3312*
* The minimum number of galleons needed for *wand(age = 40, power = 5) = 7587*
* The minimum number of galleons needed for *wand(age = 40, power = 7) = 6018*
  
The data for wands of age 20 (code 4):

![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458540035-d950b9c900-ScreenShot2016-03-21at11.23.25AM.png)

* The minimum number of galleons needed for *wand(age = 20, power = 5) = 504*
* The minimum number of galleons needed for *wand(age = 20, power = 6) = 7651*
* The minimum number of galleons needed for *wand(age = 20, power = 8) = 3688*
  
The data for wands of age 17 (code 5):

![img](https://s3.amazonaws.com/hr-challenge-images/19502/1458539700-2f319702ab-ScreenShot2016-03-21at11.23.06AM.png)

* The minimum number of galleons needed for *wand(age = 17, power = 3) = 5689*
* The minimum number of galleons needed for *wand(age = 17, power = 10) = 9897*

**Answer**

```sql
SELECT
 ID,
 AGE,
 COINS_NEEDED,
 POWER
FROM WANDS W
JOIN WANDS_PROPERTY WP
 ON W.CODE = WP.CODE
WHERE WP.IS_EVIL = 0 AND COINS_NEEDED = (SELECT 
                                          MIN(COINS_NEEDED) 
                                         FROM WANDS AS Ws
                                         JOIN WANDS_PROPERTY AS WPs
                                          ON (Ws.CODE = WPs.CODE) 
                                         WHERE Ws.POWER = W.POWER AND WPs.AGE = WP.AGE
                                        )
ORDER BY POWER DESC, AGE DESC;
```

# 📌 **Challenges** 
  
Julia asked her students to create some coding challenges. Write a query to print the hacker_id, name, and the total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

**Input Format**

The following tables contain challenge data:

* Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker.
  
 ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521004-cb4c077dd3-ScreenShot2016-03-21at6.06.54AM.png)
 
* Challenges: The challenge_id is the id of the challenge, and hacker_id is the id of the student who created the challenge.
  
 ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521079-549341d9ec-ScreenShot2016-03-21at6.07.03AM.png)
___

**Sample Input 0**

Hackers Table: 

![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521384-34c6866dae-ScreenShot2016-03-21at6.07.15AM.png)

Challenges Table: 

![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521410-befa8e1cd9-ScreenShot2016-03-21at6.07.25AM.png)

**Sample Output 0**

    21283 Angela 6
    88255 Patrick 5
    96196 Lisa 1
    
**Sample Input 1**

Hackers Table: 

![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521469-87036deea3-ScreenShot2016-03-21at6.07.48AM.png)

Challenges Table: 

![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521490-358215cf0b-ScreenShot2016-03-21at6.07.58AM.png)

**Sample Output 1**

    12299 Rose 6
    34856 Angela 6
    79345 Frank 4
    80491 Patrick 3
    81041 Lisa 1

**Explanation**

For Sample Case 0, we can get the following details:

![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521677-fd04c384c0-ScreenShot2016-03-21at6.07.38AM.png)

Students *5077* and *62743* both created *4* challenges, but the maximum number of challenges created is *6* so these students are excluded from the result.
  
For Sample Case 1, we can get the following details:

![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521836-24039e7523-ScreenShot2016-03-21at6.08.08AM.png)

Students *12299* and *34856* both created *6* challenges. Because *6* is the maximum number of challenges created, these students are included in the result.

**Answer**

```sql
SELECT
 H.HACKER_ID, 
 H.NAME, 
 COUNT(C.CHALLENGE_ID) AS TOTAL
FROM HACKERS H
JOIN CHALLENGES C 
 ON H.HACKER_ID = C.HACKER_ID
GROUP BY H.HACKER_ID, H.NAME
HAVING TOTAL = (SELECT
                 MAX(TOTAL) AS MAX_TOTAL
                FROM (SELECT
                       COUNT(Cs.CHALLENGE_ID) AS TOTAL
                      FROM CHALLENGES Cs
                      GROUP BY Cs.HACKER_ID) AS CRACK
               ) OR TOTAL IN (SELECT
                               DISTINCT TOTAL AS T_UNIQUE
                              FROM (SELECT 
                                     Hs.HACKER_ID, 
                                     Hs.NAME, 
                                     COUNT(CHALLENGE_ID) AS TOTAL
                                    FROM HACKERS Hs
                                    JOIN CHALLENGES Cs 
                                     ON Cs.HACKER_ID = Hs.HACKER_ID
                                    GROUP BY Hs.HACKER_ID, Hs.NAME
                                   ) COUNTS
                              GROUP BY TOTAL
                              HAVING COUNT(TOTAL) = 1
                              )
ORDER BY TOTAL DESC, C.HACKER_ID;
```

# 📌 **Contest Leaderboard**
On Progress... (Unsolved)
