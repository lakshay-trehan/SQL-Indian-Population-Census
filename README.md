# SQL-Indian-Population-Census

QUES -1 Find out no of rows into dataset
SELECT COUNT(*) FROM CENSUS ;
SELECT COUNT(*) FROM POPULATION ;

QUES -2 CALCULATE THE DATASET FOR JHARKHAND AND BIHAR 
SELECT * FROM CENSUS
WHERE STATE IN ('JHARKHAND','BIHAR') 

QUES-3 FIND THE TOTAL POPULATION OF INDIA 
SELECT * FROM POPULATION ;
SELECT SUM(POPULATION) AS TOTAL_POPULATION  
FROM POPULATION ;

QUES -4 What is the average growth of india ?
SELECT AVG(GROWTH)*100  FROM CENSUS;

QUES -5 what is average growth of all the states?
SELECT * FROM CENSUS;
SELECT STATE , AVG(GROWTH)*100 FROM CENSUS
GROUP BY STATE ;
QUES-6 What is the average sex ratio of all the states ?
SELECT * FROM CENSUS ;
SELECT STATE, ROUND(AVG(SEX_RATIO),0)  FROM CENSUS
GROUP BY STATE
ORDER BY AVG(SEX_RATIO) DESC;

QUES -7 What is average sex ratio of all the states sort by desc ?
SELECT STATE, ROUND(AVG(SEX_RATIO),0)  FROM CENSUS
GROUP BY STATE
ORDER BY AVG(SEX_RATIO) DESC;

ques- 8 what is the average literacy rate of all the states and sort it by desc ?
SELECT * FROM CENSUS ;
SELECT STATE, ROUND( AVG(LITERACY) ,0) FROM CENSUS 
GROUP BY STATE 
ORDER BY AVG(LITERACY) DESC ;
QUES - 9 what is the average literacy rate of all the states and sort it by desc and also find out the state having avg literacy rate>90
SELECT STATE, ROUND( AVG(LITERACY) ,0) FROM CENSUS 
GROUP BY STATE HAVING ROUND( AVG(LITERACY) ,0)>90
ORDER BY AVG(LITERACY) DESC ;

QUES -10 What are the top 3 states with highest growth percentage ?
SELECT STATE , ROUND( AVG(GROWTH)*100,0) FROM CENSUS
GROUP BY STATE 
ORDER BY AVG(GROWTH) DESC limit 3 ;
USE CENSUS
QUES - 11 Calculate the no of males and females in dataset ?
SELECT s.state , sum(s.males) as total_males , sum(s.females) as total_females from
(SELECT d.district, d.state, round(d.population/(d.sex_ratio +1),0) males , round(d.population*d.sex_ratio/(d.sex_ratio +1),0) females FROM
(SELECT c.District , c.state , c.growth ,c.sex_ratio/1000 as sex_ratio ,c.literacy,p.population FROM CENSUS c INNER JOIN POPULATION P 
ON c.district = p.district) d) s
group by s.state ;

QUES - 12 Calculate the total literacy rate
SELECT * FROM CENSUS ;
SELECT s. state , sum(s.literatepeople) as total_literatepeople , sum(s.illiteratepeople) as total_illiteratepeople FROM
(SELECT d.district, d.state , round(d.literacy_ratio*d.population,0) literatepeople,round((1-d.literacy_ratio)* d.population,0) illiteratepeople FROM
(SELECT c.District , c.state , c.growth ,c.literacy/100 as literacy_ratio ,p.population FROM CENSUS c INNER JOIN POPULATION P 
ON c.district = p.district) d) s
GROUP BY s.state ;
