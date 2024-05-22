# Revising the Select Query I 
  
Query all columns for all American cities in the CITY table with populations larger than 100000. The CountryCode for America is USA.

The CITY table is described as follows:  

![img]([https://s3.amazonaws.com/hr-challenge-images/12887/1443815629-ac2a843fb7-1.png](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg))    
  
	SELECT 
	CASE 
	WHEN (A + B <= C) OR (B + C <= A) OR(A + C <= B) THEN 'Not A Triangle'
	WHEN (A = B) AND (B = C) THEN 'Equilateral'
	WHEN (A
