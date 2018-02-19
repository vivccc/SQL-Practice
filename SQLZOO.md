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


