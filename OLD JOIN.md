#  Solutions for SQL Zoo Questions  
## Aggregrate Functions Tutorial

---
### The Table Tennis Olympics Database
--
###  Table Preview

<img width="1231" height="708" alt="image" src="https://github.com/user-attachments/assets/4734c18b-ffa2-4493-82ec-325dd74656a6" />

---


###  Question 1:
**Task: Show the athelete (who) and the country name for medal winners in 2000.**

```sql
SELECT who, country.name
FROM ttms
JOIN country
         ON (ttms.country=country.id)
WHERE games = 2000;
```

###  Question 2:
**Task: Show the who and the color of the medal for the medal winners from 'Sweden'.**

```sql
SELECT who, color
FROM ttms
JOIN country ON ttms.country = country.id
WHERE name = 'Sweden';
```

###  Question 3:
**Task: Show the years in which 'China' won a 'gold' medal.**

```sql
SELECT games
FROM ttms
JOIN country ON ttms.country = country.id
WHERE name = 'China' AND color = 'gold';
```

### Women's Singles Table Tennis Olympics Database
--
###  Table Preview

<img width="1307" height="301" alt="image" src="https://github.com/user-attachments/assets/ed1090c4-4df4-4bb7-947f-dfd064743a84" />

---

###  Question 4:
**Task: Show who won medals in the 'Barcelona' games.**

```sql
SELECT who
  FROM ttws JOIN games
            ON (ttws.games=games.yr)
  WHERE city = 'Barcelona';
```

###  Question 5: 
**Task: Show which city 'Jing Chen' won medals. Show the city and the medal color.**

```sql
SELECT city, color
FROM ttws JOIN games
            ON (ttws.games=games.yr)
WHERE who = 'Jing Chen';
```

###  Question 6: 
**Task: Show who won the gold medal and the city.**

```sql
SELECT who, city
FROM ttws JOIN games
            ON (ttws.games=games.yr)
WHERE color = 'gold';
```

### Women's Singles Table Tennis Olympics Database
--
###  Table Preview

<img width="1306" height="411" alt="image" src="https://github.com/user-attachments/assets/60a86ea7-00af-47d5-9774-d24e9aa91fb4" />

---

###  Question 7: 
**Task: Show the games and color of the medal won by the team that includes 'Yan Sen'.**

```sql
SELECT games, color 
FROM ttmd
    JOIN team ON ( ttmd.team= team.id)
WHERE name = 'Yan Sen';
```

###  Question 8: 
**Task: Show the 'gold' medal winners in 2004.**

```sql
SELECT name
FROM ttmd
    JOIN team ON ( ttmd.team= team.id)
WHERE color = 'gold' AND games = 2004;
```

###  Question 9: 
**Task: Show the name of each medal winner country 'FRA'.**

```sql
SELECT name
FROM ttmd
    JOIN team ON ( ttmd.team= team.id)
WHERE country = 'FRA';
```




