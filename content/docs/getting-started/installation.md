---
title: "Installation"
weight: 6
toc: true
---

In order to generate the code at compiletime, SQLComponents has to be added as a build plugin ( under  `build > plugins` in `pom.xml` ) along with the corresposing JDBC driver.

```xml
<plugin>
	<groupId>org.sqlcomponents</groupId>
	<artifactId>maven-plugin</artifactId>
	<version>1.0-SNAPSHOT</version>
	<executions>
		<execution>
			<phase>generate-sources</phase>
			<goals>
				<goal>generate</goal>
			</goals>
		</execution>
	</executions>
	<dependencies>
		<dependency>
			<groupId>org.postgresql</groupId>
			<artifactId>postgresql</artifactId>
			<version>${postgresql.version}</version>
		</dependency>
	</dependencies>
</plugin>
```
