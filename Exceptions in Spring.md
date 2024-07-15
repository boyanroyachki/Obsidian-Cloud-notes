### Exception Handling in Spring

Exception handling in Spring can be managed at various levels, from simple try-catch blocks to sophisticated exception handling mechanisms provided by the framework. Spring provides a consistent approach to handling exceptions in RESTful services and MVC web applications through annotations and configurations.

### Basic Concepts

1. **Exception Hierarchy in Java:**
   - **Checked Exceptions:** These are exceptions that are checked at compile-time (e.g., `IOException`, `SQLException`). They must be declared in the method signature or handled within the method.
   - **Unchecked Exceptions:** These include runtime exceptions (`RuntimeException` and its subclasses) and errors (`Error` and its subclasses), which are not checked at compile-time.

2. **Spring Exception Handling Mechanisms:**
   - **@ExceptionHandler:** Used to handle exceptions in specific controller classes or across all controllers.
   - **@ControllerAdvice:** Provides a global exception handling mechanism across all controllers.
   - **ResponseEntityExceptionHandler:** A convenient base class for @ControllerAdvice classes to handle standard Spring exceptions.

### Example Implementations

#### 1. Using @ExceptionHandler

This annotation is used within a controller to handle exceptions that occur within that controller.

```java
@RestController
public class UserController {

    @GetMapping("/user/{id}")
    public User getUser(@PathVariable String id) {
        if ("unknown".equals(id)) {
            throw new UserNotFoundException("User not found with id: " + id);
        }
        return new User(id, "John Doe");
    }

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFoundException(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```

#### 2. Using @ControllerAdvice

This annotation allows you to handle exceptions globally, across all controllers.

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFoundException(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGenericException(Exception ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

#### 3. Custom Exception Class

Creating custom exceptions to use in your application.

```java
public class UserNotFoundException extends RuntimeException {
    public UserNotFoundException(String message) {
        super(message);
    }
}
```

#### 4. Using ResponseEntityExceptionHandler

You can extend `ResponseEntityExceptionHandler` to handle common Spring exceptions.

```java
@ControllerAdvice
public class CustomGlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @Override
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex,
                                                                  HttpHeaders headers,
                                                                  HttpStatus status,
                                                                  WebRequest request) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error -> 
            errors.put(error.getField(), error.getDefaultMessage()));

        return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
    }

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFoundException(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```

#### 5. Custom Response Structure

You can customize the response structure for exceptions.

```java
public class ErrorResponse {
    private String message;
    private List<String> details;

    public ErrorResponse(String message, List<String> details) {
        this.message = message;
        this.details = details;
    }

    // Getters and setters
}

@ControllerAdvice
public class CustomExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public final ResponseEntity<ErrorResponse> handleUserNotFoundException(UserNotFoundException ex, WebRequest request) {
        List<String> details = Arrays.asList(ex.getMessage());
        ErrorResponse error = new ErrorResponse("User Not Found", details);
        return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Exception.class)
    public final ResponseEntity<ErrorResponse> handleAllExceptions(Exception ex, WebRequest request) {
        List<String> details = Arrays.asList(ex.getMessage());
        ErrorResponse error = new ErrorResponse("Server Error", details);
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

### References

- **Spring Documentation on Exception Handling:** [Spring Framework Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-ann-exceptionhandler)
- **Baeldung's Guide to Exception Handling in Spring:** [Exception Handling in Spring Boot REST API](https://www.baeldung.com/exception-handling-for-rest-with-spring)
- **JavaTpoint's Spring Exception Handling Tutorial:** [Spring Exception Handling](https://www.javatpoint.com/spring-boot-exception-handling)

These resources provide detailed insights and further examples to help you implement exception handling in your Spring applications effectively.