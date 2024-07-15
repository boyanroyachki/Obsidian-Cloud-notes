Here’s a sample README for your Java BCrypt Decoder project:

---

# Java BCrypt Decoder

Java BCrypt Decoder is a simple Java application that attempts to crack a given bcrypt hash using a wordlist. The application leverages parallel processing to optimize the cracking process.

## Features

- **BCrypt Hash Cracking**: Given a bcrypt hash, the program attempts to find the original password from a provided wordlist.
- **Parallel Processing**: Utilizes Java's `CompletableFuture` and `ExecutorService` to speed up the cracking process by distributing the work across multiple CPU cores.
- **User Input**: Prompts the user to input the bcrypt hash and the path to the wordlist file.
- **Time Measurement**: Outputs the time taken to find the password or confirm that it is not in the wordlist.

## Requirements

- Java 8 or higher
- `jBCrypt` library

## Dependencies

Make sure to include the `jBCrypt` dependency in your `pom.xml` if you are using Maven:

```xml
<dependency>
    <groupId>de.svenkubiak</groupId>
    <artifactId>jBCrypt</artifactId>
    <version>0.4</version>
</dependency>
```

## Usage

1. **Clone the repository**:
   ```sh
   git clone https://github.com/your-username/Java-BCrypt-Decoder.git
   cd Java-BCrypt-Decoder
   ```

2. **Compile the program**:
   ```sh
   javac -cp .;path\to\jBCrypt.jar org/commodolink/Main.java
   ```

3. **Run the program**:
   ```sh
   java -cp .;path\to\jBCrypt.jar org.commodolink.Main
   ```

4. **Provide inputs**:
   - Paste the bcrypt hash when prompted.
   - Provide the path to the wordlist file.

## Example

Here is an example of how to use the program:

```sh
$ java -cp .;path\to\jBCrypt.jar org.commodolink.Main

*  Paste password hash here: 
$2a$12$0BQSb2aEt3ERVUxNl2OW2uM3bP6PTRGo9L8SstYE9JsJwTx.PCGV2

** Paste path to wordlist here: 
C:\path\to\wordlist.txt

Wordlist loaded. Number of words: 10000
Password found: password123
Time taken: 1234 milliseconds
```

## Code

Here is the main code for the program:

```java
package org.commodolink;

import org.mindrot.jbcrypt.BCrypt;

import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;
import java.util.Scanner;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.Executors;
import java.util.concurrent.ExecutorService;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("\n\n");

        System.out.println("*  Paste password hash here: ");
        String hash = scanner.nextLine().trim();

        System.out.println("** Paste path to wordlist here: ");
        String path = scanner.nextLine().trim();

        long startTime = System.currentTimeMillis();

        List<String> wordlist = null;
        while (true) {
            Path filePath = Paths.get(path);
            if (Files.exists(filePath) && Files.isReadable(filePath)) {
                try {
                    wordlist = Files.readAllLines(filePath);
                    if (!wordlist.isEmpty()) {
                        System.out.println("Wordlist loaded. Number of words: " + wordlist.size());
                        break;
                    } else {
                        System.out.println("Wordlist is empty! Please provide a valid wordlist.");
                    }
                } catch (Exception e) {
                    System.out.println("Error reading the wordlist: " + e.getMessage());
                }
            } else {
                System.out.println("File not found or not readable! Please provide a valid path.");
            }

            System.out.println("** Retype path: ");
            path = scanner.nextLine().trim();
        }

        ExecutorService executor = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());

        List<CompletableFuture<Boolean>> futures = wordlist.stream()
                .map(word -> CompletableFuture.supplyAsync(() -> {
                    if (BCrypt.checkpw(word, hash)) {
                        long endTime = System.currentTimeMillis();
                        long elapsedTime = endTime - startTime;
                        System.out.println("Password found: " + word);
                        System.out.println("Time taken: " + elapsedTime + " milliseconds");
                        return true;
                    }
                    return false;
                }, executor))
                .collect(Collectors.toList());

        try {
            boolean passwordFound = false;
            for (CompletableFuture<Boolean> future : futures) {
                if (future.get()) {
                    passwordFound = true;
                    break;
                }
            }
            if (!passwordFound) {
                long endTime = System.currentTimeMillis();
                long elapsedTime = endTime - startTime;
                System.out.println("Password not found in the wordlist.");
                System.out.println("Time taken: " + elapsedTime + " milliseconds");
            }
        } catch (InterruptedException | ExecutionException e) {
            System.out.println("Error during password cracking: " + e.getMessage());
        } finally {
            executor.shutdown();
        }
    }
}
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

This README provides a clear and structured guide for users to understand, set up, and use your Java BCrypt Decoder project. It includes sections for features, requirements, dependencies, usage, an example, the main code, contributing, and the license.