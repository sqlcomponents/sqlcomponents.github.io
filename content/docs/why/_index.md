---
title: "Why SQL Components"
weight: 1
toc: true
---

Before diving into the "why," let’s first understand the problem SQL Components aims to solve.

> Consider a simple Java application that connects to a relational database like PostgreSQL to create a movie store.

The database schema looks like this:

```sql
CREATE TABLE movie (
    id smallserial PRIMARY KEY,
    title VARCHAR(80),
    directed_by VARCHAR(80)
);
```

Now, let's add some movies:

```sql
INSERT INTO movie (title, directed_by) VALUES
        ('Inception', 'Christopher Nolan'),
        ('Pulp Fiction', 'Quentin Tarantino'),
        ('The Matrix', 'Lana Wachowski'),
        ('Dunkirk', 'Christopher Nolan'),
        ('Fight Club', 'David Fincher'),
        ('Interstellar', 'Christopher Nolan'),
        ('The Social Network', 'David Fincher'),
        ('The Dark Knight', 'Christopher Nolan');
```

Suppose you want to list the movies directed by `Christopher Nolan`. As a Java developer, your responsibilities include:

1. Managing database connections
2. Creating model or DTO classes
3. Implementing Data Access Objects (DAO)

Over the years, various Java frameworks have addressed these challenges in different ways. In the following sections, we’ll explore how these frameworks approach the problem and how SQL Components provides a unique solution.