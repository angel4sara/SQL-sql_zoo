#  Solutions for SQL Zoo Questions  
## Aggregrate Functions Tutorial

---

###  Table Preview

<img width="1237" height="397" alt="image" src="https://github.com/user-attachments/assets/9a1204ce-196b-4c81-8721-0a10b11f02af" />

---

###  Question 1: Total world population 
**Task: Show the total population of the world.**

```sql
SELECT SUM(population) AS total_population
FROM world
```

###  Question 2: List of continents
**Task: List all the continents - just once each.**

```sql
SELECT SUM(gdp) AS GDP_of_Africa
FROM world
WHERE continent = 'Africa';
```

###  Question 3: GDP of Africa
**Task: Give the total GDP of Africa.**

```sql
SELECT name, GDP/population AS percapitaGDP
FROM world
WHERE population >= 200000000;
```

###  Question 4: Count the big countries
**Task: How many countries have an area of at least 1000000.**

```sql
SELECT COUNT(name) AS no_countries 
FROM world
WHERE area >= 1000000;
```

###  Question 5: Baltic states population
**Task: What is the total population of ('Estonia', 'Latvia', 'Lithuania').**

```sql
SELECT SUM(population) AS total_population
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania');
```

###  Question 6: Counting the countries of each continent
**Task: For each continent show the continent and number of countries.**

```sql
SELECT continent, COUNT(name) AS number_of_countries
FROM world
GROUP BY continent;
```

###  Question 7: Counting big countries in each continent
**Task: For each continent show the continent and number of countries with populations of at least 10 million.**

```sql
SELECT continent, COUNT(name) AS number_of_countries
FROM world
WHERE population >= 10000000
GROUP BY continent;
```

###  Question 8: Counting big continents
**Task: List the continents that have a total population of at least 100 million.**

```sql
SELECT continent 
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000;
```
## Nobel

###  Question 9: Toal Prizes
**Task: Show the total number of prizes awarded.**

```sql
SELECT COUNT(winner) 
FROM nobel;
```

###  Question 10:
**Task: List each subject - just once**

```sql
SELECT DISTINCT(subject)
FROM nobel;
```

###  Question 11:
**Task: Show the total number of prizes awarded for Physics.**

```sql
SELECT COUNT(subject)
FRom nobel
WHERE subject = 'Physics';
```

###  Question 12:
**Task: For each subject show the subject and the number of prizes.**

```sql
SELECT subject, COUNT(winner)
FROM nobel
GROUP BY subject;
```

###  Question 13: 
**Task:For each subject show the first year that the prize was awarded.**

```sql
SELECT subject, MIN(yr)
FROM nobel
GROUP BY subject;

```
###  Question 14:
**Task: For each subject show the number of prizes awarded in the year 2000.**

```sql
SELECT subject, COUNT(DISTINCT winner)
FROM nobel
GROUP BY subject;
```

###  Question 15:
**Task: Show the number of different winners for each subject. Be aware that Frederick Sanger has won the chemistry prize twice - he should only be counted once.**

```sql
SELECT COUNT(subject)
FRom nobel
WHERE subject = 'Physics';
```

###  Question 16:
**Task: For each subject show how many years have had prizes awarded.**

```sql
SELECT subject, COUNT(DISTINCT yr)
FROM nobel
GROUP BY subject;
```

###  Question 17: 
**Task: Show the years in which three prizes were given for Physics.**

```sql
SELECT yr
FROM nobel
WHERE subject = 'Physics'
GROUP BY yr
HAVING COUNT(winner) = 3;
```

###  Question 18:
**Task: Show winners who have won more than once.**

```sql
SELECT winner
FROM nobel
GROUP BY winner
HAVING COUNT(winner) > 1;
```

###  Question 19:
**Task: Show winners who have won more than one subject.**

```sql
SELECT winner
FROM nobel
GROUP BY winner
HAVING COUNT(DISTINCT subject) > 1;
```

###  Question 20:
**Task: Show the year and subject where 3 prizes were given. Show only years 2000 onwards.**

```sql
SELECT yr, subject
FROM nobel
WHERE yr >= 2000
GROUP BY yr,subject
HAVING COUNT(DISTINCT winner) = 3;
```


