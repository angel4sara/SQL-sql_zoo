#  Solutions for SQL Zoo Questions  
##  SELECT Basics

---

###  Table Preview

<img width="583" height="305" alt="World Table" src="https://github.com/user-attachments/assets/1f036cfa-a1ce-43eb-a861-6a9d94c36478" />

---

##  Introducing the *world* table of countries

---

###  Question 1: Show the population of Germany  
**Task: Modify the query to show the population of Germany.**

```sql
SELECT population 
FROM world
WHERE name = 'Germany';
```

###  Question 2: Show the name and the population for 'Sweden', 'Norway', and 'Denmark'
**Task: Display name and population for selected Scandinavian countries.** 

```sql
SELECT name, population
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

###  Question 2: Show countries with area between 200,000 and 250,000
**Task: Display country name and area for countries with area in the specified range.** 

```sql
SELECT name, area
FROM world
WHERE area BETWEEN 200000 AND 250000;
```

