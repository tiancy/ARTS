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

git checkout master // switch branch

git reset --soft HEAD^ // Undo a commit  
Refer to https://git-scm.com/docs/git-reset#git-reset-Undoacommitandredo
