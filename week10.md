# Techniques

## Count with if condition in mysql query

use sum() in place of count()

```SQL
select
  a.id
  sum(if(b.status=0,1,0)) as numcount
 from a
  left join b on a.id = b.id
 where a.status = 0
 group by a.id
```

Reference
[Count with if condition in mysql query](https://stackoverflow.com/questions/9798937/count-with-if-condition-in-mysql-query)
