# Technique

## Hbase

$ hbase shell

```hbase
// TABLE
list
// scan where status = 1
scan 't1', {COLUMNS => 'info:status', FILTER => "(ValueFilter(=, 'binary:1'))"}
```

## Mysql limit

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


## linux chown, chmod
```
更改文件属主，也可以同时更改文件属组
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名

$ chown tian tmp.log

r:4
w:2
x:1
$ chmod 770 tmp.log

```
Refer to https://www.w3cschool.cn/linux/linux-file-attr-permission.html
