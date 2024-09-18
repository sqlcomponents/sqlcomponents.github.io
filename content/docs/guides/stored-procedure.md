---
title: "Stored Procedure"
weight: 12
draft: false
---

> **Stored Procedures** are a powerful feature in relational databases that allow you to encapsulate SQL logic on the database side. A stored procedure is a precompiled set of one or more SQL statements that can perform complex operations like updates, inserts, and even condition handling. By moving logic into stored procedures, you can reduce the amount of database interaction from your application code, increase performance, and improve maintainability.

Here’s an example of a stored procedure to transfer funds between two accounts:

```sql
CREATE OR REPLACE PROCEDURE transfer(
   sender INT,
   receiver INT,
   amount DECIMAL
)
LANGUAGE plpgsql
AS $$
BEGIN
    -- Subtracting the amount from the sender's account
    UPDATE accounts
    SET balance = balance - amount
    WHERE id = sender;

    -- Adding the amount to the receiver's account
    UPDATE accounts
    SET balance = balance + amount
    WHERE id = receiver;

    COMMIT;
END $$;
```

This stored procedure transfers an amount from one account to another by updating the balances of both accounts.

To call this stored procedure in SQL:

```sql
CALL transfer(1, 2, 500);
```

### Using SQL Components to Call Stored Procedures

SQL Components makes it easy to call stored procedures directly from Java code without any need for complex mappings or additional libraries. Here’s how you can invoke the `transfer` stored procedure using **DatabaseManager** in SQL Components:

```java
DatabaseManager.getManager().transfer(1, 2, 500);
```