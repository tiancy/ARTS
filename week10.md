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

## mybatis sql

```SQL
select name from table where age < 20 // wrong
select name from table where age &lt; 20 // right
```

## mybatis sql allowMultiQueries

jdbc:mysql://localhost:3306/dbname?allowMultiQueries=true

```SQL
set @now = NOW();
set @now7 = DATE_ADD(@now, INTERVAL 7 DAY);
select name from table where endTime > @now AND endTime &lt; @now7;
```

## mybatis multi param

```
// mapper interface
List<Object> getList(@Param(value = "status") int status, @Param(value = "pager") Pager pager);

// mapper xml
// remove the parameterType
select * from table where status=#{status} limit #{pager.index}, #{pager.size}
```

## decompression for jar file at cmd
 
$ unzip filename.jar [-d filepath]

$ jar tvf filename.jar // list for filename.jar

## [Searching for Commands in the History](http://www.gnu.org/software/bash/manual/html_node/Searching.html)

C-r

## [Cutting cmd](https://www.howtogeek.com/howto/ubuntu/keyboard-shortcuts-for-bash-command-shell-for-ubuntu-debian-suse-redhat-linux-etc/)

C-u

## tail -- display the last part of a file

$ tail -f filename.log

## git commands

合并一个分支的之前提交的内容到另一个分支，可以将这个分支reset --soft HEAD^到之前要合并的一个版本，然后合并

git checkout master // switch branch  
git reset --soft HEAD^ // Undo a commit  
git checkout dev  
git merge master // merge branch master to current branch

References  
https://git-scm.com/docs/git-reset#git-reset-Undoacommitandredo  
https://git-scm.com/docs/git-merge

## listening ports

lsof -i -P -n | grep LISTEN  

Refer to https://www.cyberciti.biz/faq/unix-linux-check-if-port-is-in-use-command/

# Share

QPS

Query rate" redirects here. It is not to be confused with Query throughput.  
Queries per second (QPS) is a common measure of the amount of search traffic an information retrieval system, such as a search engine or a database, receives during one second.[1] The term is used more broadly for any request–response system, more correctly called requests per second (RPS).  

High-traffic systems must watch their QPS in order to know when to scale the system to handle more load.

Refer to https://en.wikipedia.org/wiki/Queries_per_second
