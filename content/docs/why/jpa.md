---
title: "JPA"
weight: 3
toc: true
---

**Java Persistence API (JPA)** is a well-known framework that abstracts most of the database interaction for Java applications by utilizing **Object-Relational Mapping (ORM)**. JPA handles both **connection management** and **DAO implementation**, leaving the developer to focus on defining **model classes** and mapping them to database tables.

With JPA, developers only need to annotate their model classes with the appropriate mappings to the database schema:

```java
@Entity
@Table(name = "movie")
public class Movie {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String title;
    
    @Column(name = "directed_by")
    private String directedBy;

    // Getters and Setters
}
```

Here’s how you would use JPA to find movies by a specific director:

```java
public class MovieRepository {
    
    @PersistenceContext
    private EntityManager entityManager;

    public List<Movie> findByDirector(String director) {
        String jpql = "SELECT m FROM Movie m WHERE m.directedBy = :director";
        return entityManager.createQuery(jpql, Movie.class)
                            .setParameter("director", director)
                            .getResultList();
    }
}
```

### SQL Components: Flexibility Beyond ORM

While JPA simplifies connection management and DAO implementation, **SQL Components** provides greater flexibility by allowing developers to go beyond simple table-to-entity mappings. With SQL Components, you can easily work with **stored procedures**, **views**, and other advanced database features that are often difficult to handle with standard ORM frameworks like JPA.

Here’s what sets SQL Components apart:

1. **No ORM Restrictions**: SQL Components allows you to fully leverage relational databases without being restricted by table-entity mapping. You can work with **stored procedures**, **views**, and even complex queries effortlessly.
   
2. **Native Java Code Generation**: Unlike JPA, which often relies on **reflection APIs** for dynamic entity handling, SQL Components generates **pure Java code** at compile-time, significantly boosting performance.

3. **Type-Safe API**: SQL Components ensures compile-time type checking, reducing runtime errors and offering more reliability.

In SQL Components, the same query to list movies directed by a particular director would look like this:

```java
List<Movie> movies = DataManager.getManager().getMovieStore()
                        .select()
                            .where(directedBy().eq("Christopher Nolan"))
                        .returning();
```

**Key Differences**:

- **Flexibility**: SQL Components supports stored procedures, views, and advanced SQL features without ORM limitations.
- **Performance**: Native Java code generation without reflection improves API performance.
- **Type Safety**: Compile-time checks ensure code correctness and reduce runtime errors.

