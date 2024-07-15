In Spring, DAOs (Data Access Objects), Services, and Beans serve distinct purposes within the application architecture. Here's a breakdown of each, along with examples to illustrate their roles:

### DAO (Data Access Object)
A DAO is a design pattern that provides an abstract interface to some type of database or other persistence mechanism. It handles the CRUD (Create, Read, Update, Delete) operations and abstracts the details of the data access logic.

**Example:**
```java
@Repository
public class UserDao {
    @Autowired
    private JdbcTemplate jdbcTemplate;

    public User getUserById(int id) {
        String sql = "SELECT * FROM users WHERE id = ?";
        return jdbcTemplate.queryForObject(sql, new Object[]{id}, new UserRowMapper());
    }

    // Other CRUD methods
}
```

### Service
A Service layer typically contains business logic and calls methods in the DAO layer. It acts as an intermediary between the controller and the DAO, orchestrating operations and ensuring that business rules are applied.

**Example:**
```java
@Service
public class UserService {
    @Autowired
    private UserDao userDao;

    public User getUserById(int id) {
        // Additional business logic can be added here
        return userDao.getUserById(id);
    }

    // Other business logic methods
}
```

### Bean
A Spring Bean is any object that is instantiated, assembled, and otherwise managed by a Spring IoC (Inversion of Control) container. Beans can be configured using XML, annotations, or Java-based configuration. Beans can be any type of object, including DAOs, services, controllers, etc.

**Example:**
```java
@Configuration
public class AppConfig {

    @Bean
    public UserService userService() {
        return new UserService();
    }

    @Bean
    public UserDao userDao() {
        return new UserDao();
    }
}
```

### Specializations of Beans
Spring provides several stereotype annotations to specialize Beans:

- `@Component`: A generic stereotype for any Spring-managed component.
- `@Repository`: A specialization of `@Component` for the persistence layer. It translates database-related exceptions into Spring's DataAccessException.
- `@Service`: A specialization of `@Component` for the service layer. It indicates that the class contains business logic.
- `@Controller`: A specialization of `@Component` for the presentation layer in Spring MVC.

### Annotations and Layering
Using these annotations helps to clearly define the roles of different classes in your application, enhancing readability and maintainability. Each annotation adds a layer-specific semantics to the component, helping Spring to manage them appropriately.

**Example Using Annotations:**
```java
@Component
public class GenericComponent {
    // General-purpose code
}

@Repository
public class ProductRepository {
    // Data access code
}

@Service
public class ProductService {
    // Business logic code
}

@Controller
public class ProductController {
    // Web layer code
}
```

By organizing your application into DAOs, Services, and annotated Beans, you create a clean separation of concerns, making your codebase more modular and easier to maintain【6†source】【7†source】【8†source】【9†source】.