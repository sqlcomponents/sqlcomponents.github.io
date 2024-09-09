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
    identifier: "Connection"
weight: 2
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

We need configure SQLComponents to connect to the database instance. we should create a file named `sql-components.yml` as given below

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

After this, you can build the project with

```sh
mvn clean package
```

once the build is suvvessful, you should see the generated code under `target > generated-sources`