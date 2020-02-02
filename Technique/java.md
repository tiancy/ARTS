## [Determining the Default Version of the JDK](https://docs.oracle.com/javase/8/docs/technotes/guides/install/mac_jdk.html#A1096875)

To run a different version of Java, either specify the full path, or use the java_home tool:

% /usr/libexec/java_home -v 1.8.0_06 --exec javac -version

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
} catch (Exception e) {
}
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

Refer to https://stackoverflow.com/questions/2793150/how-to-use-java-net-urlconnection-to-fire-and-handle-http-requests

## java Comparator

```java
class User {
    private String name;
}

List<User> users = ...;
Collections.sort(users, (e1, e2) -> {
    // return e1.name.compareTo(e2.name);
    return e2.name.length() - e1.name.length();
});
```

## java double colon ::

```
<Class name>::<method name>
```

Refer to https://www.geeksforgeeks.org/double-colon-operator-in-java/
