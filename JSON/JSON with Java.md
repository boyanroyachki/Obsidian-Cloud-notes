### Overview of JSON (JavaScript Object Notation)

JSON (JavaScript Object Notation) is a lightweight data-interchange format that's easy for humans to read and write and easy for machines to parse and generate. It is widely used for data exchange between clients and servers, particularly in web applications. JSON is text-based and can represent simple data structures and associative arrays (known as objects).

### Structure of JSON

JSON is built on two structures:
1. **A collection of name/value pairs**: In various languages, this is realized as an object, record, struct, dictionary, hash table, keyed list, or associative array.
2. **An ordered list of values**: In most languages, this is realized as an array, vector, list, or sequence.

### Example of JSON Data
```json
{
    "name": "John Doe",
    "age": 30,
    "isEmployee": true,
    "address": {
        "street": "123 Main St",
        "city": "Anytown",
        "state": "CA"
    },
    "phoneNumbers": [
        {
            "type": "home",
            "number": "123-456-7890"
        },
        {
            "type": "office",
            "number": "987-654-3210"
        }
    ]
}
```

### Working with JSON in Java

Java provides several libraries for working with JSON, including `org.json`, `Gson`, and `Jackson`. Below are examples demonstrating how to read and write JSON using these libraries.

#### Using `org.json`

**Reading JSON from a String:**
```java
import org.json.JSONObject;

public class JSONExample {
    public static void main(String[] args) {
        String jsonString = "{ \"name\": \"John Doe\", \"age\": 30, \"isEmployee\": true }";
        JSONObject jsonObject = new JSONObject(jsonString);

        String name = jsonObject.getString("name");
        int age = jsonObject.getInt("age");
        boolean isEmployee = jsonObject.getBoolean("isEmployee");

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Is Employee: " + isEmployee);
    }
}
```

**Writing JSON to a String:**
```java
import org.json.JSONObject;

public class JSONExample {
    public static void main(String[] args) {
        JSONObject jsonObject = new JSONObject();
        jsonObject.put("name", "Jane Doe");
        jsonObject.put("age", 25);
        jsonObject.put("isEmployee", false);

        String jsonString = jsonObject.toString();
        System.out.println(jsonString);
    }
}
```

#### Using Gson

**Reading JSON from a String:**
```java
import com.google.gson.Gson;

public class GsonExample {
    public static void main(String[] args) {
        String jsonString = "{ \"name\": \"John Doe\", \"age\": 30, \"isEmployee\": true }";
        Gson gson = new Gson();
        Person person = gson.fromJson(jsonString, Person.class);

        System.out.println("Name: " + person.name);
        System.out.println("Age: " + person.age);
        System.out.println("Is Employee: " + person.isEmployee);
    }

    class Person {
        String name;
        int age;
        boolean isEmployee;
    }
}
```

**Writing JSON to a String:**
```java
import com.google.gson.Gson;

public class GsonExample {
    public static void main(String[] args) {
        Person person = new Person();
        person.name = "Jane Doe";
        person.age = 25;
        person.isEmployee = false;

        Gson gson = new Gson();
        String jsonString = gson.toJson(person);
        System.out.println(jsonString);
    }

    class Person {
        String name;
        int age;
        boolean isEmployee;
    }
}
```

#### Using Jackson

**Reading JSON from a String:**
```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class JacksonExample {
    public static void main(String[] args) {
        String jsonString = "{ \"name\": \"John Doe\", \"age\": 30, \"isEmployee\": true }";
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            Person person = objectMapper.readValue(jsonString, Person.class);

            System.out.println("Name: " + person.getName());
            System.out.println("Age: " + person.getAge());
            System.out.println("Is Employee: " + person.isEmployee());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    static class Person {
        private String name;
        private int age;
        private boolean isEmployee;

        // Getters and Setters
        public String getName() { return name; }
        public void setName(String name) { this.name = name; }
        public int getAge() { return age; }
        public void setAge(int age) { this.age = age; }
        public boolean isEmployee() { return isEmployee; }
        public void setEmployee(boolean isEmployee) { this.isEmployee = isEmployee; }
    }
}
```

**Writing JSON to a String:**
```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class JacksonExample {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("Jane Doe");
        person.setAge(25);
        person.setEmployee(false);

        ObjectMapper objectMapper = new ObjectMapper();
        try {
            String jsonString = objectMapper.writeValueAsString(person);
            System.out.println(jsonString);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    static class Person {
        private String name;
        private int age;
        private boolean isEmployee;

        // Getters and Setters
        public String getName() { return name; }
        public void setName(String name) { this.name = name; }
        public int getAge() { return age; }
        public void setAge(int age) { this.age = age; }
        public boolean isEmployee() { return isEmployee; }
        public void setEmployee(boolean isEmployee) { this.isEmployee = isEmployee; }
    }
}
```

### Reading and Writing JSON from/to Files

#### Using Jackson

**Reading JSON from a File:**
```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;

public class JacksonFileExample {
    public static void main(String[] args) {
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            Person person = objectMapper.readValue(new File("person.json"),                    Person.class);
            System.out.println("Name: " + person.getName());
            System.out.println("Age: " + person.getAge());
            System.out.println("Is Employee: " + person.isEmployee());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    static class Person {
        private String name;
        private int age;
        private boolean isEmployee;

        // Getters and Setters
        public String getName() { return name; }
        public void setName(String name) { this.name = name; }
        public int getAge() { return age; }
        public void setAge(int age) { this.age = age; }
        public boolean isEmployee() { return isEmployee; }
        public void setEmployee(boolean isEmployee) { this.isEmployee = isEmployee; }
    }
}
```

**Writing JSON to a File:**
```java
import com.fasterxml.jackson.databind.ObjectMapper;
import java.io.File;

public class JacksonFileExample {
    public static void main(String[] args) {
        Person person = new Person();
        person.setName("Jane Doe");
        person.setAge(25);
        person.setEmployee(false);

        ObjectMapper objectMapper = new ObjectMapper();
        try {
            objectMapper.writeValue(new File("person.json"), person);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    static class Person {
        private String name;
        private int age;
        private boolean isEmployee;

        // Getters and Setters
        public String getName() { return name; }
        public void setName(String name) { this.name = name; }
        public int getAge() { return age; }
        public void setAge(int age) { this.age = age; }
        public boolean isEmployee() { return isEmployee; }
        public void setEmployee(boolean isEmployee) { this.isEmployee = isEmployee; }
    }
}
```

### Conclusion

JSON is a versatile and widely used data format for data interchange. Java provides several robust libraries like `org.json`, Gson, and Jackson for working with JSON data. These libraries make it easy to parse JSON from strings and files, and to serialize Java objects into JSON format. By leveraging these libraries, developers can seamlessly integrate JSON data handling into their Java applications.