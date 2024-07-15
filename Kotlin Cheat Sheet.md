### The Ultimate Kotlin Cheat Sheet

#### 1. **Basic Syntax**

**Hello World:**
```kotlin
fun main() {
    println("Hello, World!")
}
```

**Data Types:**
- Basic Types: `Int`, `Double`, `Float`, `Long`, `Short`, `Byte`, `Boolean`, `Char`, `String`

**Variables:**
```kotlin
val readOnly: String = "Hello"  // Immutable variable
var mutable: String = "World"   // Mutable variable
```

**String Interpolation:**
```kotlin
val name = "Kotlin"
println("Hello, $name!")
```

**Control Statements:**
- **If-Else:**
  ```kotlin
  val a = 10
  val b = 20
  val max = if (a > b) a else b
  ```

- **When (Switch Case):**
  ```kotlin
  val x = 1
  when (x) {
      1 -> println("One")
      2 -> println("Two")
      else -> println("Other")
  }
  ```

- **For Loop:**
  ```kotlin
  for (i in 1..10) {
      println(i)
  }
  ```

- **While Loop:**
  ```kotlin
  var i = 0
  while (i < 10) {
      println(i)
      i++
  }
  ```

#### 2. **Functions**

**Basic Function:**
```kotlin
fun add(a: Int, b: Int): Int {
    return a + b
}
```

**Single Expression Function:**
```kotlin
fun add(a: Int, b: Int): Int = a + b
```

**Default Arguments:**
```kotlin
fun greet(name: String = "World") {
    println("Hello, $name!")
}
```

**Named Arguments:**
```kotlin
fun formatText(text: String, size: Int, color: String) {
    // ...
}

formatText(size = 12, color = "Red", text = "Hello")
```

#### 3. **Classes and Objects**

**Class Declaration:**
```kotlin
class Car(val color: String, val model: String) {
    fun drive() {
        println("Driving $color $model")
    }
}
```

**Inheritance:**
```kotlin
open class Vehicle(val brand: String) {
    open fun start() {
        println("Starting vehicle")
    }
}

class Car(brand: String, val model: String) : Vehicle(brand) {
    override fun start() {
        println("Starting car")
    }
}
```

**Data Classes:**
```kotlin
data class User(val name: String, val age: Int)
```

**Singleton (Object Declaration):**
```kotlin
object Database {
    fun connect() {
        println("Connected to database")
    }
}
```

#### 4. **Collections**

**List:**
```kotlin
val numbers: List<Int> = listOf(1, 2, 3, 4, 5)
```

**Mutable List:**
```kotlin
val mutableNumbers: MutableList<Int> = mutableListOf(1, 2, 3)
mutableNumbers.add(4)
```

**Set:**
```kotlin
val items: Set<String> = setOf("Apple", "Banana", "Cherry")
```

**Map:**
```kotlin
val map: Map<String, Int> = mapOf("Alice" to 25, "Bob" to 30)
```

#### 5. **Lambda Expressions and Higher-Order Functions**

**Lambda Expression:**
```kotlin
val sum = { a: Int, b: Int -> a + b }
println(sum(1, 2))
```

**Higher-Order Function:**
```kotlin
fun operateOnNumbers(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}

val result = operateOnNumbers(4, 2, sum)
```

#### 6. **Kotlin Coroutines**

**Basic Coroutine:**
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

**Async and Await:**
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    val deferred = async {
        delay(1000L)
        "Async Result"
    }
    println("Result: ${deferred.await()}")
}
```

#### 7. **Extensions**

**Extension Function:**
```kotlin
fun String.removeWhitespace(): String {
    return this.replace("\\s".toRegex(), "")
}

val text = "Hello World"
println(text.removeWhitespace())
```

#### 8. **Null Safety**

**Nullable Types:**
```kotlin
var nullableString: String? = "Hello"
nullableString = null
```

**Safe Call Operator:**
```kotlin
println(nullableString?.length)
```

**Elvis Operator:**
```kotlin
val length = nullableString?.length ?: 0
```

**Non-Null Assertion:**
```kotlin
println(nullableString!!.length)
```

#### 9. **Standard Library Functions**

**Apply:**
```kotlin
val car = Car("Red", "Toyota").apply {
    color = "Blue"
    model = "Honda"
}
```

**Let:**
```kotlin
nullableString?.let {
    println(it)
}
```

**Also:**
```kotlin
val numbers = mutableListOf(1, 2, 3).also {
    println("Original: $it")
}
```

**Run:**
```kotlin
val length = "Hello".run {
    this.length
}
```

**With:**
```kotlin
val result = with(car) {
    color = "Green"
    model = "Tesla"
}
```

#### 10. **Testing with JUnit**

**Basic JUnit Test:**
```kotlin
import org.junit.Test
import kotlin.test.assertEquals

class CalculatorTest {

    @Test
    fun testAddition() {
        val calc = Calculator()
        val result = calc.add(2, 3)
        assertEquals(5, result)
    }
}

class Calculator {
    fun add(a: Int, b: Int): Int = a + b
}
```

### References

- [Official Kotlin Documentation](https://kotlinlang.org/docs/home.html)
- [Kotlin Programming by Example (Book)](https://www.packtpub.com/product/kotlin-programming-by-example/9781788474542)
- [Kotlin Coroutines Guide](https://kotlinlang.org/docs/coroutines-guide.html)
- [Baeldung's Guide to Kotlin](https://www.baeldung.com/kotlin)

This cheat sheet provides a comprehensive overview of key concepts, syntax, and features in Kotlin, making it a handy reference for both beginners and experienced developers.