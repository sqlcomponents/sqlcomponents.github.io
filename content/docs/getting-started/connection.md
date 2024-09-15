---
title: "Connection"
weight: 7
toc: true
---

We need configure SQLComponents to connect to the database instance. we should create a file named `sql-components.yml` as given below

```yml
# Connection Details
name: Sample
url: "jdbc:postgresql://localhost:5432/sampledb"
userName: "user"
password: "password"
schemaName: "sampledb"
```

After this, you can build the project with

```sh
mvn clean package
```

once the build is suvvessful, you should see the generated code under `target > generated-sources`
