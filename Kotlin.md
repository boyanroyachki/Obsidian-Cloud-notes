### Kotlin 101: A Basic Yet Detailed Lesson

#### 1. **Introduction to Kotlin**
Kotlin is a statically typed, cross-platform programming language developed by JetBrains. It is fully interoperable with Java and runs on the Java Virtual Machine (JVM). Kotlin is widely used for Android development and is known for its concise syntax and improved safety features compared to Java.

#### 2. **Basic Syntax and Structure**
- **Variables:**
  ```kotlin
  val immutable = "Hello, World!"  // Read-only variable
  var mutable = "Hello, Kotlin!"   // Mutable variable
  ```
  `val` is used for read-only variables, and `var` is used for mutable variables.

- **Functions:**
  ```kotlin
  fun greet(name: String): String {
      return "Hello, $name!"
  }
  ```
  Functions in Kotlin are declared using the `fun` keyword, and string interpolation is done using `$`.

- **Control Structures:**
  ```kotlin
  fun max(a: Int, b: Int): Int {
      return if (a > b) a else b
  }
  ```
  Kotlin uses traditional control structures like `if`, `when`, `for`, and `while`.

#### 3. **Key Features**
- **Null Safety:** Kotlin's type system is designed to eliminate NullPointerExceptions (NPE) from your code.
  ```kotlin
  var name: String? = "John"
  name = null  // Allowed
  ```
  Use `?` to mark a variable as nullable.

- **Extension Functions:** Allows you to add functionality to existing classes.
  ```kotlin
  fun String.removeWhitespace(): String {
      return this.replace("\\s".toRegex(), "")
  }
  ```
  You can call this function on any `String` object.

- **Data Classes:** Simplifies the creation of classes that are primarily used to hold data.
  ```kotlin
  data class User(val name: String, val age: Int)
  ```

- **Higher-order Functions and Lambdas:** Functions that take other functions as parameters or return functions.
  ```kotlin
  fun calculate(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
      return operation(a, b)
  }
  val sum = calculate(5, 3) { x, y -> x + y }
  ```

#### 4. **Advanced Topics**
- **Coroutines:** Simplifies asynchronous programming. Kotlin's coroutines are lightweight threads.
  ```kotlin
  import kotlinx.coroutines.*

  fun main() = runBlocking {
      launch {
          delay(1000L)
          println("World!")
      }
      println("Hello,")
  }
  ```

- **Type Inference:** Kotlin can infer types automatically.
  ```kotlin
  val number = 42  // Inferred as Int
  ```

- **Smart Casts:** Kotlin performs automatic type casts when it is safe to do so.
  ```kotlin
  fun demo(x: Any) {
      if (x is String) {
          println(x.length)  // x is automatically cast to String
      }
  }
  ```

#### 5. **Interoperability with Java**
Kotlin is designed to be fully interoperable with Java, allowing you to call Java code from Kotlin and vice versa.
```kotlin
// Calling a Java method from Kotlin
val javaString: java.lang.String = "Hello, Java"
```

#### 6. **Common Use Cases**
- **Android Development:** Kotlin is officially supported by Google for Android development.
- **Server-side Development:** Kotlin can be used for developing server-side applications, leveraging frameworks like Ktor.
- **Script Writing:** Kotlin scripts can be used for small automation tasks.

#### 7. **Example Project: Simple Kotlin Application**
Here is a simple Kotlin application that demonstrates basic syntax and features:
```kotlin
fun main() {
    val user = User("Alice", 30)
    println(user)

    val greeting = greet("Kotlin")
    println(greeting)

    val sum = calculate(10, 5) { a, b -> a + b }
    println("Sum: $sum")

    println("Without whitespace: ${"Kotlin is fun".removeWhitespace()}")
}
```
This code snippet demonstrates the use of data classes, functions, higher-order functions, and extension functions.

### Conclusion
Kotlin is a modern, versatile language that simplifies many aspects of programming compared to Java. It is particularly useful for Android development but also shines in server-side development and scripting. Understanding its basic syntax, key features, and interoperability with Java will help you in technical interviews and real-world applications.

For more detailed information and resources, you can visit:
- [Hackr.io's Kotlin Interview Questions](https://hackr.io/blog/kotlin-interview-questions)
- [DevInterview.io's Kotlin Interview Questions](https://devinterview.io/)
- [Android Developers' Kotlin Basics](https://developer.android.com/kotlin/learn)

These resources will provide further insights and examples to solidify your understanding of Kotlin.