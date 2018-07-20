# Tip

## [RANKING IN MYSQL RESULTS](https://stackoverflow.com/questions/2520357/mysql-get-row-number-on-select)
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

## spring @RequestBody

```Java
@RequestMapping("/list")
public List<Object> list(@RequestBody Object obj) {
    // data...
    return null;
}
```
Headers Content-Type=application/json <br/>
Body {}, then request params is null, if it were otherwise, would be error HttpMessageNotReadableException: Required request body is missing

## set terminal color
export PS1="\[\e[30;1m\]\u@\h:\w\$\[\e[m\] "
alias ls='ls -G'