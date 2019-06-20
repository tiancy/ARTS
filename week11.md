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

## java URLConnection

```java
Map<String, String> heads = new HashMap<>();
heads.put("Content-Type", "application/x-www-form-urlencoded;charset=UTF-8");

HttpURLConnection conn =  (HttpURLConnection) new URL(url).openConnection();
conn.setRequestMethod("POST");
conn.setDoOutput(true);
conn.setDoInput(true);
// conn.setRequestProperty("Content-Type", heads.get("Content-Type")); // get null, why? key?!
conn.setRequestProperty("Content-Type", "application/x-www-form-urlencoded;charset=UTF-8");

String query = "name=tian&nick=tian";
OutputStream out = conn.getOutputStream();
out.write(query.getBytes("UTF-8"));
out.flush();
out.close();

BufferedReader reader = new BufferedReader(new InputStreamReader(conn.getInputStream()));
String line;
StringBuffer sb = new StringBuffer();
while ((line = reader.readLine()) != null) {
    sb.append(line);
}
```
