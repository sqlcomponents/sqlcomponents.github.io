---
title: "Store"
description: "Guides lead a user through a specific task they want to accomplish, often with a sequence of steps."
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "example-6a1a6be4373e933280d78ea53de6158e"
weight: 3
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

SQLComponents can be added as a build plugin. Also we need to add JDBC driver. for example if we need to work with postgres database we should add

```xml
<build>
		<plugins>
    ---
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
      ---
      </plugins>
</build>
		
```