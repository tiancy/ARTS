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
     