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
/** INSERT INTO movie 
 *      VALUES('Inception', 'Christopher Nolan')
 * /
movieStore
    .insert()
        .values(new Movie(null, "Inception", "Christopher Nolan"))
    .execute(dataSource);
```

We need to insert multiple records to the table.

```
/**
INSERT INTO movie (title, directed_by)
        VALUES ('Pulp Fiction', 'Quentin Tarantino'),
        ('The Matrix', 'Lana Wachowski'),
        ('Dunkirk', 'Christopher Nolan'),
        ('Fight Club', 'David Fincher'),
        ('Interstellar', 'Christopher Nolan'),
        ('The Social Network', 'David Fincher');
*/
movieStore
    .insert()
        values(new Movie(null, "Pulp Fiction", "Quentin Tarantino"),
            new Movie(null, "The Matrix", "Lana Wachowski")
            new Movie(null, "Dunkirk", "Christopher Nolan"),
            new Movie(null, "Fight Club", "David Fincher"),
            new Movie(null, "Interstellar", "Christopher Nolan"),
            new Movie(null, "The Social Network", "David Fincher"))
    .execute(dataSource);
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
                        .execute(dataSource);
```

We need to select the movies with where clause

```java
List<Movie> movies = movieStore
                        .select()
                            .where(directedBy().eq("Christopher Nolan"))
                        .execute(dataSource);
```

We need to select a movie by primary key (id columns)

```java
Movie movie = movieStore
                        .select()
                        .execute(dataSource);
```


We need to select a movie by primary key (id columns) with where clause

```java
Movie movie = movieStore
                        .select()
                        .where(directedBy().eq("Christopher Nolan"))
                        .execute(dataSource);
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
    .execute(dataSource);
```

Update a record with multiple where clause

```java

//  UPDATE movie 
//      SET title='Blood Diamond', directed_by='Martyn Scorsese' 
//      WHERE id=1 AND title='Fight Club'
movieStore
    .update()
        .set(new Movie(null, "Blood Diamond", "Martyn Scorsese"))
        .where(
            id().eq(1).and()
            .title().eq("Fight Club"))
    .execute(dataSource);
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
    .execute(dataSource);
```


## Delete

Delete all the records in the table

```java
movieStore
    .delete()
    .execute(dataSource);
```


We need to delete the movies with where clause

```java
movieStore
    .delete()
        .where(directedBy().eq("Christopher Nolan"))
    .execute(dataSource);
```