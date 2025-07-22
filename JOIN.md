#  Solutions for SQL Zoo Questions  
## Aggregrate Functions Tutorial

---

###  Table Preview

<img width="768" height="689" alt="image" src="https://github.com/user-attachments/assets/2671c43f-1a39-438a-8d2b-4477315c3f65" />

<img width="653" height="617" alt="image" src="https://github.com/user-attachments/assets/161287a4-6de3-4be6-906b-61fa045f7160" />


---

JOIN and UEFA EURO 2012
--- 
This tutorial introduces JOIN which allows you to use data from two or more tables. The tables contain all matches and goals from UEFA EURO 2012 Football Championship in Poland and Ukraine.

###  Question 1:
**Task: The first example shows the goal scored by a player with the last name 'Bender'. The * says to list all the columns in the table - a shorter way of saying matchid, teamid, player, gtime
Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'**

```sql
SELECT matchid, player
FROM goal 
WHERE teamid ='GER';
```

###  Question 2:
**Task: From the previous query you can see that Lars Bender's scored a goal in game 1012. Now we want to know what teams were playing in that match.
Notice in the that the column matchid in the goal table corresponds to the id column in the game table. We can look up information about game 1012 by finding that row in the game table.
Show id, stadium, team1, team2 for just game 1012**

```sql
SELECT id,stadium,team1,team2
FROM game
WHERE id = 1012;
```

###  Question 3:
**Task: Modify it to show the player, teamid, stadium and mdate for every German goal.**

```sql
SELECT player, teamid, stadium, mdate
FROM game 
JOIN goal ON (game.id=goal.matchid)
WHERE teamid = 'GER';
```

###  Question 4:
**Task: Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'.**

```sql
SELECT team1, team2, player
FROM game
JOIN goal ON (game.id=goal.matchid)
WHERE player LIKE 'Mario%'
```

###  Question 5: 
**Task: Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10.**

```sql
SELECT player, teamid, coach, gtime
FROM goal
JOIN eteam on goal.teamid = eteam.id 
WHERE gtime<=10;
```

###  Question 6: 
**Task: List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.**

```sql
SELECT mdate, teamname
FROM game
JOIN eteam ON (team1 = eteam.id)
WHERE coach = 'Fernando Santos';
```

###  Question 7: 
**Task: List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'**

```sql
SELECT player
FROM goal
JOIN game ON (goal.matchid = game.id)
WHERE stadium = 'National Stadium, Warsaw';
```

###  Question 8: 
**Task: Show the name of all players who scored a goal against Germany.**

```sql
SELECT DISTINCT player
FROM goal
JOIN game ON goal.matchid = game.id
WHERE (game.team1 = 'GER' OR game.team2 = 'GER')
 AND goal.teamid != 'GER';
```

###  Question 9: 
**Task: Show teamname and the total number of goals scored.**

```sql
SELECT teamname, COUNT(teamid)
FROM eteam 
JOIN goal ON id=teamid
GROUP BY teamname;
```

###  Question 10:
**Task: Show the stadium and the number of goals scored in each stadium.**

```sql
SELECT stadium, COUNT(teamid)
FROM game
JOIN goal ON id = matchid
GROUP BY stadium;
```

###  Question 11:
**Task: For every match involving 'POL', show the matchid, date and the number of goals scored.**

```sql
SELECT matchid, mdate, COUNT(teamid)
FROM game 
JOIN goal ON matchid = id 
WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate;
```

###  Question 12:
**Task: For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'.**

```sql
SELECT matchid, mdate, COUNT(*)
FROM game
JOIN goal ON game.id = goal.matchid
WHERE teamid = 'GER'
GROUP BY matchid, mdate;
```

###  Question 13: 
**Task: List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.
mdate	team1	score1	team2	score2
1 July 2012	ESP	4	ITA	0
10 June 2012	ESP	1	ITA	1
10 June 2012	IRL	1	CRO	3
...
Notice in the query given every goal is listed. If it was a team1 goal then a 1 appears in score1, otherwise there is a 0. You could SUM this column to get a count of the goals scored by team1. Sort your result by mdate, matchid, team1 and team2.**

```sql
SELECT mdate,
       team1, SUM(CASE WHEN teamid = team1 THEN 1 ELSE 0 END) AS score1, 
       team2, SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score2
FROM game
LEFT JOIN goal ON game.id = goal.matchid
GROUP BY mdate, matchid, team1, team2;
```


