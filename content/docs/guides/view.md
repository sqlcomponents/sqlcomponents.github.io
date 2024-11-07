---
title: "View"
weight: 11
draft: false
---

View will act as inteface for all the SQL operations againts views. For.eg For Movie view, you can get the Store from DataManages as given below

```java
MovieView movieView = DataManager.getManager().getMovieView();
```

## Materialized View

We can refresh Materialized View

```java
movieView.refresh(dataSource);
```
