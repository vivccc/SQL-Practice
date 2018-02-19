1. Find the capital and the name where the capital includes the name of the country
```
select name, capital from world
  where capital like concat('%', name, '%');
```
2. Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.
```
select winner, subject from nobel 
  where yr = 1984
  order by subject in ('Chemistry', 'Physics'), winner, subject;
```
3. Find the largest country (by area) in each continent, show the continent, the name and the area (correlated or synchronized sub-query)
```
select continent, name, area from world x
  where area >= all(
    select area from world y
      where x.continent = y.continent)
        and area > 0;
```
4. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.
```
select name, continent, population from world
  where continent not in (
    select continent from world
      where population > 25000000);
```
```
select name, continent, population from world as x
  where 25000000 > all(
    select population from world as y
      where x.continent = y.continent);
``` 

5. The WHERE clause filters rows before the aggregation, the HAVING clause filters after the aggregation.
6. List every match with the goals scored by each team as shown. Notice in the query given every goal is listed. If it was a team1 goal then a 1 appears in score1, otherwise there is a 0. You could SUM this column to get a count of the goals scored by team1. Sort your result by mdate, matchid, team1 and team2.

| mdate | team1 | score1 | team2 | score2|
|-------|:-----:|:------:|:-----:|:-----:|
|1 July 2012|ESP|4|ITA|0|
|10 June 2012|ESP|1|ITA|1|
|10 June 2012|IRL|1|CRO|3|

```
select mdate, team1, sum(case when teamid = team1 then 1 else 0 end) as score1, 
  team2, sum(case when teamid = team2 then 1 else 0 end) as score2 
  from game left join goal on (game.id = goal.matchid)
  group by mdate, team1, team2
  order by mdate, matchid, team1, team2
```
**_why using join (instead of left join), the score1=score2=0 cases are dropped???_**
