### DAO in Spring

#### Definition
DAO stands for Data Access Object. It is a design pattern used to encapsulate the data access logic and provides an abstract interface to the database. The primary purpose of a DAO is to separate the low-level data accessing API or operations from high-level business services.

#### Key Characteristics

1. **Encapsulation of Data Access Logic:**
   - DAOs provide a clean interface for database operations, hiding the complexities of the underlying data access technologies (like JDBC, Hibernate, JPA) from the business logic.

2. **Separation of Concerns:**
   - By using DAOs, the business logic is separated from data access code, leading to cleaner, more maintainable, and testable code.

3. **Abstraction:**
   - DAOs abstract the data access operations, which means any changes in the database structure or underlying database technology can be managed within the DAO layer without impacting the rest of the application.

#### Example of DAO in Spring

```java
@Repository
public class UserDao {
    
    @Autowired
    private JdbcTemplate jdbcTemplate;

    public User findById(int id) {
        String sql = "SELECT * FROM users WHERE id = ?";
        return jdbcTemplate.queryForObject(sql, new Object[]{id}, new BeanPropertyRowMapper<>(User.class));
    }

    public List<User> findAll() {
        String sql = "SELECT * FROM users";
        return jdbcTemplate.query(sql, new BeanPropertyRowMapper<>(User.class));
    }

    public int save(User user) {
        String sql = "INSERT INTO users (name, email) VALUES (?, ?)";
        return jdbcTemplate.update(sql, user.getName(), user.getEmail());
    }
}
```

### DAO vs. Service

#### DAO (Data Access Object):

- **Purpose:** Encapsulates the data access logic, providing a clean and abstract interface for database operations.
- **Focus:** Database interactions and CRUD (Create, Read, Update, Delete) operations.
- **Example Methods:** `save()`, `findById()`, `findAll()`, `update()`, `delete()`.
- **Annotations:** Typically annotated with `@Repository` in Spring to indicate that the class is a DAO component.

#### Service:

- **Purpose:** Encapsulates the business logic of the application. It can use DAOs to perform database operations as part of its logic.
- **Focus:** Business operations and use cases, orchestrating the interaction between multiple DAOs and other services.
- **Example Methods:** `createUser()`, `getUserProfile()`, `processOrder()`.
- **Annotations:** Typically annotated with `@Service` in Spring to indicate that the class is a service component.

#### Example of Service in Spring

```java
@Service
public class UserService {

    @Autowired
    private UserDao userDao;

    public User getUserById(int id) {
        return userDao.findById(id);
    }

    public List<User> getAllUsers() {
        return userDao.findAll();
    }

    public void createUser(User user) {
        userDao.save(user);
    }
}
```

### Differences

1. **Role and Responsibility:**
   - **DAO:** Directly deals with database operations.
   - **Service:** Handles business logic and workflows, often using one or more DAOs to perform required data operations.

2. **Scope of Functionality:**
   - **DAO:** Limited to data access and manipulation.
   - **Service:** Broader scope, implementing business rules, validations, and complex interactions between various system components.

3. **Reusability and Modularity:**
   - **DAO:** Can be reused across different services for consistent data access operations.
   - **Service:** Combines DAOs and other services to fulfill business requirements, promoting modularity in business logic.

### Summary
The DAO pattern in Spring helps in separating data access logic from business logic, making the application more modular and maintainable. While DAOs focus on database operations, services encapsulate business logic, often leveraging DAOs to handle data access requirements. Together, they form a layered architecture that promotes separation of concerns and code reusability.