---
title: "SQL Builders"
weight: 2
toc: true
---

**SQL Builders** are tools designed to simplify database interaction by abstracting away complex SQL queries and connection management. They help developers focus on writing business logic rather than handling raw SQL queries manually. Modern tools like **Spring Boot 3 JdbcClient** allow developers to construct and execute SQL queries programmatically with a fluent, readable API.

Out of the three main responsibilities—connection management, model/DTO creation, and DAO implementation—SQL Builders primarily remove the burden of **connection management** from developers.

When using the **Spring Boot 3 JdbcClient**, developers are still responsible for creating:

- **Model classes**
- **Data Access Objects (DAO)** using the fluent Client API
- **Row Mapping logic** (though `JdbcClient` simplifies this with `query().row(...)`)

Here is a sample of how this works using the **Spring Boot 3 JdbcClient**:

```java
// Model class
public record Movie(Long id, String title, String directedBy) {}

// DAO using Spring Boot 3 JdbcClient
@Repository
public class MovieRepository {

    private final JdbcClient jdbcClient;

    public MovieRepository(JdbcClient jdbcClient) {
        this.jdbcClient = jdbcClient;
    }

    public List<Movie> findMoviesByDirector(String director) {
        return jdbcClient.sql("SELECT id, title, directed_by FROM movie WHERE directed_by = :director")
                .param("director", director)
                .query((rs, rowNum) -> new Movie(
                    rs.getLong("id"),
                    rs.getString("title"),
                    rs.getString("directed_by")
                ))
                .list();
    }
}
```

### SQL Components: A Type-Safe Alternative

While `JdbcClient` offers a much cleaner fluent API than the older `JdbcTemplate`, **SQL Components** goes further by providing a **fully type-safe API** and eliminating the need to write any manual code for models, DAOs, or RowMappers.

Here is how you achieve the same functionality using SQL Components:

```java
List<Movie> movies = DataManager.getManager().getMovieStore()
                        .select()
                            .where(directedBy().eq("Christopher Nolan"))
                        .returning();
```

**Key Differences**:

1. **Zero Boilerplate**: Models, Store classes, and mapping logic are generated automatically from your schema.
2. **True Type-Safety**: Queries are constructed using generated metadata, ensuring that column names and types are checked at compile-time.
3. **Framework Independence**: Operates as pure Java code. While it works perfectly with Spring, it doesn't require it, making your persistence layer portable across any Java environment.