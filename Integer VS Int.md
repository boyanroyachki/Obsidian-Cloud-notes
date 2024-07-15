In Java, `Integer` and `int` represent two different types:

1. **`int`:**
   - **Primitive Type:** `int` is a primitive data type.
   - **Memory Usage:** It uses 32 bits (4 bytes) of memory.
   - **Performance:** Operations with `int` are faster because it is a simple, low-level data type.
   - **Usage:** `int` is used when you need to store a simple integer value.

   ```java
   int x = 5;
   ```

2. **`Integer`:**
   - **Wrapper Class:** `Integer` is a class that wraps a primitive `int` in an object.
   - **Memory Usage:** It consumes more memory due to object overhead.
   - **Performance:** Slightly slower compared to `int` due to additional layers of abstraction.
   - **Usage:** `Integer` is used when you need an object to represent an integer value, such as when working with collections (e.g., `ArrayList<Integer>`), or when you need to utilize methods provided by the `Integer` class.

   ```java
   Integer y = 5;
   ```

**Key Differences:**

- **Nullability:** `int` cannot be null, whereas `Integer` can be null. This is useful in cases where you need to represent the absence of a value.
  
  ```java
  Integer z = null;  // Valid
  int a = null;      // Compilation error
  ```

- **Autoboxing and Unboxing:** Java automatically converts between `int` and `Integer` in certain situations, known as autoboxing and unboxing.

  ```java
  Integer b = 10;    // Autoboxing: int to Integer
  int c = b;        // Unboxing: Integer to int
  ```

- **Methods:** `Integer` provides several utility methods, like `parseInt`, `toString`, and `valueOf`.

  ```java
  int num = Integer.parseInt("123");   // Converts a string to int
  String str = Integer.toString(123);  // Converts an int to string
  ```

In summary, use `int` for simple, performance-critical tasks involving primitive integers, and `Integer` when you need an object representation of an integer, especially when working with Java's collection framework or when nullability is required.

