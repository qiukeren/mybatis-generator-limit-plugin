# In all

Use version 1.0.4.

# mybatis-generator-limit-plugin
A MyBatis Generator plugin for MySQL pagination use limit.

Forked and modified from [叉烧包's maven plugin](https://github.com/wucao/mybatis-generator-limit-plugin)

Modified as follows:

* The origin just support xml mapper, does not support annotation java sql provider. Extended it. 
* Put into maven repository.

## Usage

Add the plugin `<plugin type="com.qiukeke.mybatis.plugins.MySQLLimitPlugin"></plugin>` into MyBatis Generator configuration file.

```
<generatorConfiguration>
    <context id="mysqlgenerator" targetRuntime="MyBatis3">
    	<plugin type="com.qiukeke.mybatis.plugins.MySQLLimitPlugin"></plugin>
    	...
    </context>
</generatorConfiguration>
```

### Running with Maven

pom.xml


```
<build>
	<plugins>
		<plugin>
			<groupId>org.mybatis.generator</groupId>
			<artifactId>mybatis-generator-maven-plugin</artifactId>
			<version>1.3.2</version>
			<dependencies>
				<dependency>
					<groupId>mysql</groupId>
					<artifactId>mysql-connector-java</artifactId>
					<version>5.1.34</version>
				</dependency>
				<dependency>
					<groupId>com.qiukeke</groupId>
					<artifactId>mybatis-generator-plugin</artifactId>
					<version>1.0.4</version>
				</dependency>
			</dependencies>
			<configuration>
				<overwrite>true</overwrite>
			</configuration>
		</plugin>
	</plugins>
</build>
```

Run `mvn mybatis-generator:generator` to generate java and xml files.

### Using the Generated Objects

```
XxxExample example = new XxxExample();
...
example.setLimit(10); // page size limit
example.setOffset(20); // offset
List<Xxx> list = xxxMapper.selectByExample(example);
```

If you use xml mapper, the SQL will be:
`select ... limit 20, 10`

If you use annotation mapper, the SQL will be:
`select ... limit 10 offset 20`


```
XxxExample example = new XxxExample();
...
example.setLimit(10); // limit
List<Xxx> list = xxxMapper.selectByExample(example);
```
If you use xml mapper, the SQL will be:
`select ... limit 10`

If you use annotation mapper, the SQL will be:
`select ... limit 10`

### Download

