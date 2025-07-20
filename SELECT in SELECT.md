#  Solutions for SQL Zoo Questions  
## SELECT within SELECT Tutorial
---

###  Table Preview

<img width="586" height="289" alt="image" src="https://github.com/user-attachments/assets/939c55a5-a289-44a4-9701-89ada7de9569" />

---

###  Question 1: Bigger than Russia
**Task: List each country name where the population is larger than that of 'Russia'.**

```sql
SELECT name 
FROM world
WHERE population >
       (SELECT population 
        FROM world
        WHERE name ='Russia');
```

###  Question 2: Richer than UK
**Task: Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.**

```sql
SELECT name
FROM world
WHERE continent = 'Europe' AND gdp/population>
       (SELECT gdp/population  AS percapitagdp
        FROM world
        WHERE name ='United Kingdom');
```

###  Question 3: Neighbours of Argentina and Australia
**Task: Which country has a population that is more than United Kingdom but less than Germany? Show the name and the population.**

```sql
SELECT name, continent
FROM world
WHERE continent IN
            (SELECT continent
             FROM world
             WHERE name IN('Argentina', 'Australia'))
ORDER BY name;
```

###  Question 4: Between Canada and Poland
**Task: Give the name of the 'peace' winners since the year 2000, including 2000.**

```sql
SELECT name, population
FROM world
WHERE population > (SELECT population
                  FROM world
                  WHERE name = 'United Kingdom')
AND 
population < (SELECT population
                  FROM world
                  WHERE name = 'Germany');
```

###  Question 5: Percentages of Germany
**Task: Germany (population roughly 80 million) has the largest population of the countries in Europe. Austria (population 8.5 million) has 11% of the population of Germany. Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
The format should be Name, Percentage for example:.**

```sql
SELECT name, CONCAT(CAST(ROUND(population/
              (SELECT population
               FROM world
               WHERE name ='Germany') *100,0)
               AS int), '%') AS percentage
FROM world
WHERE continent = 'Europe' ;
```

###  Question 6: Bigger than every country in Europe
**Task: Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)**

```sql
SELECT name
FROM world
WHERE gdp > ALL(SELECT MAX(gdp)
                 FROM world
                 WHERE continent='Europe');
```

###  Question 7: Largest in each continent
**Task: Find the largest country (by area) in each continent, show the continent, the name and the area: The above example is known as a correlated or synchronized sub-query.**

```sql
SELECT continent, name, area 
FROM world AS outer_world
WHERE area >= ALL
    (SELECT area 
     FROM world AS inner_world
     WHERE inner_world.continent = outer_world.continent);
```

###  Question 8: First country of each continent (alphabetically)
**Task: List each continent and the name of the country that comes first alphabetically.**

```sql
SELECT continent, name 
FROM world AS outer_world
WHERE name = (
              SELECT MIN(name)
              FROM world AS inner_world
              WHERE inner_world.continent = outer_world.continent);
```

###  Question 9
**Task: Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.**

```sql
SELECT name, continent, population
FROM world
WHERE continent IN(
          SELECT continent
          FROM world
          GROUP BY continent
          HAVING MAX(population) <=25000000);
```

###  Question 10: Three time bigger
**Task: Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.**

```sql
SELECT name, continent
FROM world AS outer_world
WHERE population > ALL (
    SELECT population * 3
    FROM world AS inner_world
    WHERE inner_world.continent = outer_world.continent
      AND inner_world.name != outer_world.name);
```


