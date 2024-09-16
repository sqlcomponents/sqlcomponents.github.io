---
title: "Table"
weight: 10
draft: false
---

Store will act as inteface for all the SQL operations againts tables. For.eg For Movie table, you can get the Store from DataManages as given below

```java
MovieStore movieStore = DataManager.getManager().getMovieStore();
```

From here you can execute SQL Statements against the table as follows

## Insert

We need to insert a single record to the table.

```java
// INSERT INTO movie VALUES('Inception', 'Christopher Nolan')
movieStore
    .insert()
        .values(new Movie(null, "Inception", "Christopher Nolan"))
    .execute();
```

We need to insert multiple records to the table.

```
movieStore
    .insert()
        .values(new Movie(null, "Pulp Fiction", "Quentin Tarantino"))
        .values(new Movie(null, "The Matrix", "Lana Wachowski"))
        .values(new Movie(null, "Dunkirk", "Christopher Nolan"))
        .values(new Movie(null, "Fight Club", "David Fincher"))
        .values(new Movie(null, "Interstellar", "Christopher Nolan"))
        .values(new Movie(null, "The Social Network", "David Fincher"))
    .execute();
```

We need to insert a single record to the table and return inserted value.

```java
Movie movie = movieStore
                .insert()
                    .values(new Movie(null, "The Dark Knight", "Christopher Nolan"))
                .returning();
```

## Select

We need to select all the movies

```java
List<Movie> movies = movieStore
                        .select()
                        .execute();
```

We need to select the movies with where clause

```java
List<Movie> movies = movieStore
                        .select()
                            .where(directedBy().eq("Christopher Nolan"))
                        .execute();
```

## Update

Update a record with where clause

```java

//  UPDATE movie 
//      SET title='Fight Club', directed_by='Martyn Scorsese' 
//      WHERE title='Fight Club'
movieStore
    .update()
            .set(new Movie(null, "Fight Club", "Martyn Scorsese"))
    .where(title().eq("Fight Club"))
    .execute();
```

Update a record with multiple where clause

```java

//  UPDATE movie 
//      SET title='Blood Diamond', directed_by='Martyn Scorsese' 
//      WHERE id=1 AND title='Fight Club'
movieStore
    .update()
            .set(new Movie(null, "Blood Diamond", "Martyn Scorsese"))
    .where(id().eq(1).and().title().eq("Fight Club"))
    .execute();
```

Update a record with multiple where clause amd selected columns

```java

//  UPDATE movie 
//      SET directed_by='Martyn Scorsese' 
//      WHERE id=1 AND title='Fight Club'
movieStore
    .update()
            .set(directedBy("Martyn Scorsese"))
    .where(id().eq(1).and().title().eq("Fight Club"))
    .execute();
```


## Delete

Delete all the records in the table

```java
movieStore
    .delete()
    .execute();
```

