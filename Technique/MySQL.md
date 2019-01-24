## Required Storage and Range for Integer Types Supported by MySQL

Type | Storage (Bytes) | Minimum Value Signed |	Minimum Value Unsigned | Maximum Value Signed	| Maximum Value Unsigned
--- | --- | --- | --- | --- | ---
TINYINT | 1 | -128 | 0 | 127 | 255
SMALLINT |	2 |	-32768 | 0 | 32767 | 65535
MEDIUMINT |	3 |	-8388608 | 0 | 8388607 | 16777215
INT | 4 | -2147483648 | 0 | 2147483647 | 4294967295
BIGINT | 8 | -2^63 | 0 | 2^63-1 | 2^64-1

## [utf8_unicode_ci vs utf8_general_ci by MySQL](https://forums.mysql.com/read.php?103,187048,188748#msg-188748)

### utf8_general_ci is a very simple collation. 

What it does - it just 
* removes all accents 
* then converts to upper case 
* uses the code of this sort of "base letter" result letter to compare. 

For example, these Latin letters: ÀÁÅåāă (and all other Latin letters "a" 
with any accents and in any cases) are all compared as equal to "A". 

### utf8_unicode_ci

* utf8_unicode_ci supports so called expansions and ligatures.
* utf8_unicode_ci is *generally* more accurate for all scripts. 

**The disadvantage of utf8_unicode_ci is that it is a little bit 
slower than utf8_general_ci.**

So when you need better sorting order - use utf8_unicode_ci, 
and when you utterly interested in performance - use utf8_general_ci

## force index
select id from table force index(PRI/index)

## [RANKING IN MySQL RESULTS](https://stackoverflow.com/questions/2520357/mysql-get-row-number-on-select)
```SQL
SELECT 
    rank
FROM
    (SELECT 
        @rank:=@rank + 1 AS rank, id
    FROM
        table_name t, (SELECT @rank:=0) r
    WHERE
         `order` >= (select `order` from table_name where id = 4) -- exclude id =4 after data
    ORDER BY `order` DESC) tmp
WHERE
    id = 4
```

## MySQL table data import

Table data export for insert on the Navicat,  then create temp same table,  execute insert,
data export for temp table to csv by your want, data import csv, configure import settings

## [safe update mode by mysql](https://stackoverflow.com/questions/11448068/mysql-error-code-1175-during-update-in-mysql-workbench)

Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.

Fixed Error

Try:

SET SQL_SAFE_UPDATES = 0;

Or you can modify your query to follow the rule (use primary key in where clause).

## [MySQL DISTINCT](https://dev.mysql.com/doc/refman/8.0/en/distinct-optimization.html)

```sql
SELECT DISTINCT t.a FROM t;
```

## [MySQL EXPLAIN](https://dev.mysql.com/doc/refman/8.0/en/explain.html)

The DESCRIBE and EXPLAIN statements are synonyms. In practice, the DESCRIBE keyword is more often used to obtain information about table structure, whereas EXPLAIN is used to obtain a query execution plan (that is, an explanation of how MySQL would execute a query).

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

## MySQL JOIN WHERE

```SQL
-- tableA all data
select name from tableA
  left join
  tableB on tableA.id = tableB.aid and tableB.status = 1
where tableA.status = 1

-- tableA all data, but where is tableB.status = 1 (tableB base)
select name from tableA
  left join
  tableB on tableA.id = tableB.aid
where tableA.status = 1 and tableB.status = 1
```

## MySQL limit

```mysql
-- base
SELECT 
    a.*
FROM
    t1 a
LIMIT 1000000 , 20;

-- good
SELECT 
    a.*
FROM
    t1 a,
    (SELECT 
        id
    FROM
        t1
    LIMIT 1000000 , 20) b
WHERE
    a.id = b.id;
```

Refer to https://www.toutiao.com/a6648823317069300228/?tt_from=mobile_qq&utm_campaign=client_share&timestamp=1548288913&app=news_article&utm_source=mobile_qq&iid=58523200744&utm_medium=toutiao_ios&group_id=6648823317069300228
