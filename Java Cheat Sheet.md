### The Ultimate Java Cheat Sheet

#### 1. **Basic Syntax**

**Hello World:**
```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

**Data Types:**
- Primitive: `int`, `byte`, `short`, `long`, `float`, `double`, `boolean`, `char`
- Non-primitive: `String`, Arrays, Classes, Interfaces

**Variables:**
```java
int number = 10;
String text = "Hello";
```

**Operators:**
- Arithmetic: `+`, `-`, `*`, `/`, `%`
- Relational: `==`, `!=`, `>`, `<`, `>=`, `<=`
- Logical: `&&`, `||`, `!`
- Assignment: `=`, `+=`, `-=`, `*=`, `/=`

**Control Statements:**
- **If-Else:**
  ```java
  if (condition) {
      // code
  } else if (condition) {
      // code
  } else {
      // code
  }
  ```

- **Switch:**
  ```java
  switch (variable) {
      case value1:
          // code
          break;
      case value2:
          // code
          break;
      default:
          // code
  }
  ```

- **Loops:**
  ```java
  // For loop
  for (int i = 0; i < 10; i++) {
      // code
  }

  // While loop
  while (condition) {
      // code
  }

  // Do-While loop
  do {
      // code
  } while (condition);
  ```

#### 2. **Object-Oriented Programming (OOP)**

**Classes and Objects:**
```java
public class Car {
    // fields
    String color;
    int speed;

    // constructor
    public Car(String color, int speed) {
        this.color = color;
        this.speed = speed;
    }

    // method
    public void display() {
        System.out.println("Color: " + color + ", Speed: " + speed);
    }

    public static void main(String[] args) {
        Car car1 = new Car("Red", 100);
        car1.display();
    }
}
```

**Inheritance:**
```java
class Vehicle {
    protected String brand = "Ford";
}

class Car extends Vehicle {
    private String model = "Mustang";
    public static void main(String[] args) {
        Car myCar = new Car();
        System.out.println(myCar.brand + " " + myCar.model);
    }
}
```

**Polymorphism:**
```java
class Animal {
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog();
        myAnimal.sound();
    }
}
```

**Abstraction:**
```java
abstract class Animal {
    public abstract void sound();
}

class Dog extends Animal {
    public void sound() {
        System.out.println("Dog barks");
    }
}
```

**Encapsulation:**
```java
public class Person {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

#### 3. **Collections Framework**

**List:**
```java
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
```

**Set:**
```java
Set<String> set = new HashSet<>();
set.add("Apple");
set.add("Banana");
```

**Map:**
```java
Map<String, Integer> map = new HashMap<>();
map.put("Apple", 1);
map.put("Banana", 2);
```

#### 4. **Java 8 Features**

**Lambda Expressions:**
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println(name));
```

**Streams:**
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squares = numbers.stream()
    .map(n -> n * n)
    .collect(Collectors.toList());
```

**Optional:**
```java
Optional<String> optional = Optional.of("Hello");
optional.ifPresent(System.out::println);
```

#### 5. **Exception Handling**

**Try-Catch:**
```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
} finally {
    System.out.println("This block is always executed");
}
```

**Custom Exception:**
```java
class CustomException extends Exception {
    public CustomException(String message) {
        super(message);
    }
}

public class Main {
    public static void main(String[] args) {
        try {
            throw new CustomException("Custom error occurred");
        } catch (CustomException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

#### 6. **Multithreading**

**Creating Threads:**
```java
// By extending Thread class
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}

// By implementing Runnable interface
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable is running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();

        Thread t2 = new Thread(new MyRunnable());
        t2.start();
    }
}
```

#### 7. **File I/O**

**Reading a File:**
```java
import java.nio.file.*;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        try {
            List<String> lines = Files.readAllLines(Paths.get("file.txt"));
            lines.forEach(System.out::println);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**Writing to a File:**
```java
import java.nio.file.*;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        List<String> lines = Arrays.asList("Hello, World!", "Java File I/O");
        try {
            Files.write(Paths.get("file.txt"), lines);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### 8. **Networking**

**Creating a Socket:**
```java
import java.io.*;
import java.net.*;

public class Main {
    public static void main(String[] args) {
        try (Socket socket = new Socket("localhost", 8080)) {
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));

            out.println("Hello, server");
            String response = in.readLine();
            System.out.println("Server response: " + response);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**Creating a Server:**
```java
import java.io.*;
import java.net.*;

public class Main {
    public static void main(String[] args) {
        try (ServerSocket serverSocket = new ServerSocket(8080)) {
            System.out.println("Server is listening on port 8080");
            Socket socket = serverSocket.accept();

            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

            String message = in.readLine();
            System.out.println("Client message: " + message);
            out.println("Hello, client");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### 9. **JUnit Testing**

**Basic JUnit Test:**
```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class CalculatorTest {

    @Test
    public void testAddition() {
        Calculator calc = new Calculator();
        int result = calc.add(2, 3);
        assertEquals(5, result);
    }
}

class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

### References

- [Oracle Java Documentation](https://docs.oracle.com/javase/tutorial/)
- [Baeldung Java Tutorials](https://www.baeldung.com/)
- [JavaTpoint Java Tutorial](https://www.javatpoint.com/java-tutorial)

This cheat sheet provides a comprehensive overview of key concepts, syntax, and features in Java, making it a handy reference for both beginners and experienced developers.