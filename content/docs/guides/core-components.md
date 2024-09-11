---
title: "Core Components"
weight: 9
draft: false
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
