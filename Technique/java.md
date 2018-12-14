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

## [Difference between decimal, float and double](https://stackoverflow.com/questions/618535/difference-between-decimal-float-and-double-in-net)

* float and double are floating binary point types.
* decimal is a floating decimal point type. 

As for what to use when:

* For values which are "naturally exact decimals" 
* For values which are more artefacts of nature which can't really be measured exactly anyway, float/double are more appropriate. 

## Java Regexp Replace

```Java
"?name,?name,".reqlaceAll("\\?[^,]+", "tian")
```

## [guava charmatcher](https://github.com/google/guava/wiki/StringsExplained#charmatcher)

```Java
CharMatcher.anyOf(",").trimFrom(",a,b,,c,) // return a,b,,c
```
