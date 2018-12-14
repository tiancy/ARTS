## [MyBatis Generator](http://www.mybatis.org/generator/index.html)

1.  [MyBatis GeneratorXML Configuration File Reference](http://www.mybatis.org/generator/configreference/xmlconfig.html)
2.  maven dependency
     ```
     <dependency>
         <groupId>org.mybatis.generator</groupId>
         <artifactId>mybatis-generator-core</artifactId>
         <version>1.3.5</version>
     </dependency>
     ```
3.  Run java
     ```java
     List<String> warnings = new ArrayList<String>();
     boolean overwrite = true;
     File configFile = new File("tmp/generatorConfig.xml");
     ConfigurationParser cp = new ConfigurationParser(warnings);
     Configuration config = cp.parseConfiguration(configFile);
     DefaultShellCallback callback = new DefaultShellCallback(overwrite);
     MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config, callback, warnings);
     myBatisGenerator.generate(null);
     ```
     
## mybatis like

* select column from table where column like concat(#{selectContent}, '%'), 查询条件中使用函数会影响性能
* select column from table where column like '${selectContent}%', 可能会导致sql注入

## [mybatis #{name} vs ${name}](http://www.mybatis.org/mybatis-3/sqlmap-xml.html#select)

* **#{id}**
This tells MyBatis to create a PreparedStatement parameter. With JDBC, such a parameter would be identified by a "?" in SQL passed to a new PreparedStatement, something like this:

```java
// Similar JDBC code, NOT MyBatis…
String selectPerson = "SELECT * FROM PERSON WHERE ID=?";
PreparedStatement ps = conn.prepareStatement(selectPerson);
ps.setInt(1,id);
```

* **${alias}**
This element can be used to define a reusable fragment of SQL code that can be included in other statements. It can be statically (during load phase) parametrized. Different property values can vary in include instances. For example:

```sql
<sql id="userColumns"> ${alias}.id,${alias}.username,${alias}.password </sql>
The SQL fragment can then be included in another statement, for example:

<select id="selectUsers" resultType="map">
  select
    <include refid="userColumns"><property name="alias" value="t1"/></include>,
    <include refid="userColumns"><property name="alias" value="t2"/></include>
  from some_table t1
    cross join some_table t2
</select>
```

* String Substitution

By default, using the #{} syntax will cause MyBatis to generate PreparedStatement properties and set the values safely against the PreparedStatement parameters (e.g. ?). While this is safer, faster and almost always preferred, sometimes you just want to directly inject an unmodified string into the SQL Statement. For example, for ORDER BY, you might use something like this:

ORDER BY ${columnName}
Here MyBatis won't modify or escape the string.

**NOTE** It's not safe to accept input from a user and supply it to a statement unmodified in this way. This leads to potential SQL Injection attacks and therefore you should either disallow user input in these fields, or always perform your own escapes and checks.

## Do not change property in the object getting, because insert data use getting, maybe it’s not you want

## 重复数据问题

前端发现数据出现重复问题，前一页和后一页， 怀疑后端接口有问题

解决问题思路
1. 查看数据有无重复数据
2. 怀疑分页插件有问题，是否用了无序列表
3. 根据排序字段查看数据，发现排序自段的数据一样，结果导致每次返回的数据顺序不一致
4. 增加排序字段ID，问题解决

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
