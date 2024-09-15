---
title: "SQL Builders"
weight: 2
toc: true
---

**SQL Builders** are tools designed to simplify database interaction by abstracting away complex SQL queries and connection management. They help developers focus on writing business logic rather than managing database connections and handling raw SQL queries. Popular SQL Builders like **Spring JDBC** and **QueryDSL** allow developers to construct SQL queries programmatically, making code more readable and maintainable.

Out of the three main responsibilities—connection management, model/DTO creation, and DAO implementation—SQL Builders primarily remove the burden of **connection management** from developers.

For example, when using **Spring JDBC Client**, developers still need to create:

- **Model classes**
- **Data Access Objects (DAO)** using JDBC Clients
- **RowMappers** to map database results to Java objects

Here’s a sample of how this works with **Spring JDBC Client**:

```java
// Model class
public class Movie {
    private Long id;
    private String title;
    private String directedBy;
    // Getters and Setters
}

// DAO using Spring JDBC
public class MovieRepository {

    private JdbcTemplate jdbcTemplate;

    public MovieRepository(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    public List<Movie> findMoviesByDirector(String director) {
        String sql = "SELECT * FROM movie WHERE directed_by = ?";
        return jdbcTemplate.query(sql, new Object[]{director}, new RowMapper<Movie>() {
            public Movie mapRow(ResultSet rs, int rowNum) throws SQLException {
                Movie movie = new Movie();
                movie.setId(rs.getLong("id"));
                movie.setTitle(rs.getString("title"));
                movie.setDirectedBy(rs.getString("directed_by"));
                return movie;
            }
        });
    }
}
```

### SQL Components: A Type-Safe Alternative

While SQL Builders abstract connection management, **SQL Components** offers additional benefits by providing a **type-safe API** and eliminating the need for manual code related to models, DAOs, and RowMappers. Here's how you can achieve the same functionality using SQL Components:

```java
List<Movie> movies = DataManager.getManager().getMovieStore()
                        .select()
                            .where(directedBy().eq("Christopher Nolan"))
                        .returning();
```

**Key Differences**:

1. **Automatic Code Generation**: Models, DAOs, and RowMappers are generated automatically.
2. **Type-Safe API**: Compile-time error checking ensures safety and reduces runtime issues.
3. **Framework Independence**: No need for external frameworks like Spring; it’s pure Java code that can be easily integrated into any Java application.
