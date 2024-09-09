---
title: "Installation"
description: "Guides lead a user through a specific task they want to accomplish, often with a sequence of steps."
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "installation"
weight: 1
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
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
				<goal>generated-sources</goal>
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