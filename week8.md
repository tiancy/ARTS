# Tip

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
