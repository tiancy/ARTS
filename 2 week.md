# Tip

## cmd native2ascii -reverse filepath 

[native2ascii](https://native2ascii.net) Convert national language characters to and from their Unicode equivalents in plain ASCII text.

## Required Storage and Range for Integer Types Supported by MySQL

Type | Storage (Bytes) | Minimum Value Signed |	Minimum Value Unsigned | Maximum Value Signed	| Maximum Value Unsigned
--- | --- | --- | --- | --- | ---
TINYINT |	1 |	-128 | 0 | 127 | 255
SMALLINT |	2 |	-32768 |	0 |	32767 |	65535
MEDIUMINT |	3 |	-8388608 |	0 |	8388607 |	16777215
INT |	4 |	-2147483648 |	0 |	2147483647 |	4294967295
BIGINT |	8 |	-2 63 |	0 |	2 63-1 |	2 64-1

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


# Share

## [utf8_unicode_ci vs utf8_general_ci by MySQL](https://forums.mysql.com/read.php?103,187048,188748#msg-188748)

### utf8_general_ci is a very simple collation. 

What it does - it just 
* removes all accents 
* then converts to upper case 
* uses the code of this sort of "base letter" result letter to compare. 

For example, these Latin letters: ÀÁÅåāă (and all other Latin letters "a" 
with any accents and in any cases) are all compared as equal to "A". 

### utf8_unicode_ci

* utf8_unicode_ci supports so called expansions and ligatures.
* utf8_unicode_ci is *generally* more accurate for all scripts. 

**The disadvantage of utf8_unicode_ci is that it is a little bit 
slower than utf8_general_ci.**

So when you need better sorting order - use utf8_unicode_ci, 
and when you utterly interested in performance - use utf8_general_ci.
