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
