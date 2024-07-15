Java Persistence Query Language (JPQL) is an object-oriented query language defined as part of the Java Persistence API (JPA) specification. It is designed to perform database operations on persistent entities. Here is a comprehensive overview of JPQL:

### Core Features:
1. **Platform Independence:** JPQL is platform-independent, meaning it can be used with any database management system, such as MySQL or Oracle.
2. **Object-Oriented:** Unlike SQL, which operates on tables and columns, JPQL operates on Java objects and their properties.
3. **SQL-like Syntax:** JPQL's syntax resembles SQL but is tailored to work with JPA entity objects rather than database tables directly.

### Query Types:
1. **Select Queries:** Used to retrieve data from the database.
   ```java
   Query query = em.createQuery("SELECT a FROM Author a ORDER BY a.firstName, a.lastName");
   List<Author> authors = query.getResultList();
   ```
2. **Update and Delete Queries:** JPQL allows bulk updates and deletions.
   ```java
   int updated = em.createQuery("UPDATE Author a SET a.lastName = 'Smith' WHERE a.lastName = 'Doe'").executeUpdate();
   int deleted = em.createQuery("DELETE FROM Author a WHERE a.lastName = 'Smith'").executeUpdate();
   ```

### JPQL Clauses:
- **FROM:** Specifies the entity to query.
- **WHERE:** Adds conditions to filter results.
- **ORDER BY:** Sorts the results.
- **GROUP BY and HAVING:** Group results and filter grouped data, respectively.

### Joins:
JPQL supports various types of joins to combine data from multiple entities:
```java
Query query = em.createQuery("SELECT DISTINCT a FROM Author a INNER JOIN a.books b WHERE b.publisher.name = 'XYZ Press'");
List<Author> authors = query.getResultList();
```

### Scalar and Aggregate Functions:
JPQL supports functions like `MAX`, `MIN`, `AVG`, `SUM`, and `COUNT` for aggregate operations, and scalar functions like `UPPER`, `LOWER` for string manipulation.
```java
Query query = em.createQuery("SELECT MAX(e.salary) FROM Employee e");
Double maxSalary = (Double) query.getSingleResult();
```

### Named Parameters:
JPQL allows the use of named parameters in queries for better readability and maintainability.
```java
TypedQuery<Author> query = em.createQuery("SELECT a FROM Author a WHERE a.lastName = :lastName", Author.class);
query.setParameter("lastName", "Doe");
List<Author> authors = query.getResultList();
```

### Entity Manager Methods:
- **createQuery:** Used for dynamic queries.
- **createNamedQuery:** Used for named queries defined in the entity classes.

### Persistence Context:
Entities retrieved via JPQL queries can be in one of four states: new, managed, detached, or removed. Only managed entities are synchronized with the database during a transaction commit.

### Example:
Here’s a more complex example involving aggregate functions and joins:
```java
Query query = em.createQuery(
  "SELECT NEW com.example.LineItemSum(p.price, l.quantity) " +
  "FROM PurchaseOrder o " +
  "JOIN o.orderLineItems l " +
  "JOIN l.product p " +
  "JOIN p.supplier s " +
  "WHERE s.name = 'Tortuga Trading'"
);
List<LineItemSum> results = query.getResultList();
Double totalSum = results.stream().mapToDouble(LineItemSum::getResult).sum();
```

JPQL offers a robust and flexible way to interact with the database using an object-oriented approach, making it a powerful tool for developers working with JPA.

For more detailed examples and advanced usage, you can refer to sources like [JavaTpoint](https://www.javatpoint.com/jpa-jpql) and [Oracle's official documentation](https://docs.oracle.com/javaee/7/tutorial/persistence-querylanguage.htm).