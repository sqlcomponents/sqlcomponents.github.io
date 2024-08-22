---
title: "Connection"
description: "Guides lead a user through a specific task they want to accomplish, often with a sequence of steps."
summary: ""
date: 2023-09-07T16:04:48+02:00
lastmod: 2023-09-07T16:04:48+02:00
draft: false
menu:
  docs:
    parent: ""
    identifier: "example-6a1a6be4373e933280d78ea53de6158e"
weight: 2
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

Lets  connect to our database. First we need to add respective JDBC driver. for eg if we need to connect to postgres we need to add

```xml
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <version>${postgresql.version}</version>
    </dependency>
```

Next, We need configure SQLComponents to connect to our database instance. we should create file named `sql-components.yml` with below details

```yml
# Connection Details
name: Sample
url: "jdbc:postgresql://localhost:5432/sampledb"
userName: "user"
password: "password"
schemaName: "sampledb"

# Mapping Logic
rootPackage: "com.example"
```