#  Solutions for SQL Zoo Questions  
## SELECT from WORLD Tutorial

---

###  Table Preview

<img width="556" height="267" alt="image" src="https://github.com/user-attachments/assets/f1072789-307e-4539-960c-286a55043c9f" />

---

###  Question 1: Introduction 
**Task: Observe the result of running this SQL command to show the name, continent and population of all countries.**

```sql
SELECT name, continent, population
FROM world;
```
###  Question 2: Show countries with population over 200 million
**Task: Show the name for the countries that have a population of at least 200 million.**

```sql
SELECT name
FROM world
WHERE population >= 200000000;
```

###  Question 3: Per capita GDP
**Task: Give the name and the per capita GDP for those countries with a population of at least 200 million.**

```sql
SELECT name, GDP/population AS percapitaGDP
FROM world
WHERE population >= 200000000;
```

###  Question 4: South America In millions
**Task: Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.**

```sql
SELECT name, population/1000000
FROM world 
WHERE continent = 'South America';
```

###  Question 5: France, Germany, Italy
**Task: Show the name and population for France, Germany, Italy**

```sql
SELECT name, population 
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

###  Question 6: United
**Task: Show the countries which have a name that includes the word 'United'**

```sql
SELECT name
FROM world
WHERE name LIKE '%United%';
```

###  Question 7: Two ways to be big
**Task: Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.
Show the countries that are big by area or big by population. Show name, population and area.**

```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 
OR
population > 250000000;
```

###  Question 8: One or the other (but not both)
**Task: Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.
Australia has a big area but a small population, it should be included.
Indonesia has a big population but a small area, it should be included.
China has a big population and big area, it should be excluded.
United Kingdom has a small population and a small area, it should be excluded.**

```sql
SELECT name, population, area
FROM world
WHERE area > 3000000
XOR
population > 250000000;
```

###  Question 9: Rounding
**Task: Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.
For Americas show population in millions and GDP in billions both to 2 decimal places.**

```sql
SELECT name, ROUND(population/1000000,2), ROUND(GDP/1000000000,2)
FROM world
WHERE continent = 'South America';
```

###  Question 10: Trillion dollar economies
**Task: Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.
Show per-capita GDP for the trillion dollar countries to the nearest $1000.**

```sql
SELECT name, ROUND(gdp/population, -3) AS percapitaGDP
FROM world
WHERE gdp >= 1000000000000;
```

###  Question 11: Name and capital have the same length11
**Task: Greece has capital Athens. Each of the strings 'Greece', and 'Athens' has 6 characters. Show the name and capital where the name and the capital have the same number of characters.
You can use the LENGTH function to find the number of characters in a string.**

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

###  Question 12: Matching name and capital
**Task: The capital of Sweden is Stockholm. Both words start with the letter 'S'. Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word. - You can use the function LEFT to isolate the first character. - You can use <> as the NOT EQUALS operator.**

```sql
SELECT name, capital
FROM world
WHERE LEFT(name,1) = LEFT(capital,1)
AND
name <> capital;
```

###  Question 13: All the vowels
**Task: Equatorial Guinea and Dominican Republic have all of the vowels (a e i o u) in the name. They don't count because they have more than one word in the name. Find the country that has all the vowels and no spaces in its name. - You can use the phrase name NOT LIKE '%a%' to exclude characters from your results. - The query shown misses countries like Bahamas and Belarus because they contain at least one 'a'**

```sql
SELECT name
FROM world
WHERE name LIKE '%a%'
     AND name LIKE '%e%'
     AND name LIKE '%i%'
     AND name LIKE '%o%'
     AND name LIKE '%u%'
     AND name NOT LIKE '% %';
```


