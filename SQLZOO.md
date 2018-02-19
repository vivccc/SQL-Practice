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
