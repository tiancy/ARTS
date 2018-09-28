# Technique

## Convert json to string
JSON.stringify({"name":"tian"})

## Java string convert to json

```Java
ObjectMapper om = new ObjectMapper();
try {
JsonNode node = om.readTree("{\"name\":\"value\"}");
JsonNode snode = node.get("name");
if (snode != null) {
  String name = snode.asText();
}

// add
((ObjectNode)node).put("name1", "value1");
```

## [Mysql DISTINCT](https://dev.mysql.com/doc/refman/8.0/en/distinct-optimization.html)

```sql
SELECT DISTINCT t.a FROM t;
```

## [Mysql EXPLAIN](https://dev.mysql.com/doc/refman/8.0/en/explain.html)

The DESCRIBE and EXPLAIN statements are synonyms. In practice, the DESCRIBE keyword is more often used to obtain information about table structure, whereas EXPLAIN is used to obtain a query execution plan (that is, an explanation of how MySQL would execute a query).

# Share

## Go Log

```Go
f, err := os.OpenFile(time.Now().Format("2006-01-02")+".log", os.O_RDWR | os.O_CREATE | os.O_APPEND, 0666)
if err != nil {
    log.Fatalf("error opening file: %v", err)
}
defer f.Close()

log.SetOutput(f)
log.Println("This is a test log entry")
```
references
[SetOutput](https://golang.google.cn/pkg/log/#SetOutput)
[go-golang-write-log-to-file](https://stackoverflow.com/questions/19965795/go-golang-write-log-to-file)
