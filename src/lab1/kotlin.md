# Kotlin

În cele ce urmează, ne vom familiariza cu limbajul Kotlin. Kotlin este un
limbaj de programare dezvoltat de JetBrains. Kotlin este complet interoperabil
cu Java și rulează pe Java Virtual Machine (JVM). Acesta vine cu o serie de
îmbunătățiri:

* Sintaxă concisă: Kotlin reduce cantitatea de cod "boilerplate", făcând codul mai ușor de citit și de întreținut.
* Safety by design: Prin design, Kotlin elimină anumite clase de erori, cum ar fi erorile de referință nulă (NullPointerExceptions).
* Programare funcțională: Kotlin oferă suport excelent pentru programarea funcțională, inclusiv funcții de ordin superior și lambda-uri.
* Interoperabilitate cu Java: Codul Kotlin poate fi folosit alături de cod Java existent, facilitând adoptarea treptată.
* Suport pentru dezvoltare multiplataformă: Kotlin poate fi utilizat nu doar pentru dezvoltare Android, ci și pentru backend, web frontend și chiar aplicații iOS.
* Coroutine-uri: Oferă o modalitate simplificată de a gestiona operațiunile asincrone și concurența.
* Dezvoltare Android: Din 2019, Google a declarat Kotlin ca fiind limbajul preferat pentru dezvoltarea aplicațiilor Android.


**Declaratia de functii.**

```kotlin
fun calculateSum(numbers: List<Int>): Int {
    return numbers.sum()
}
```

```java
public int calculateSum(List<Integer> numbers) {
    int sum = 0;
    for (int number : numbers) {
        sum += number;
    }
    return sum;
}
```

**Data classes.**

```kotlin
data class Person(val name: String, val age: Int)
```

```java
class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters, setters, equals, hashCode, and toString methods manually implemented
}
```

**Stilul functional ca first class citizen.**

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val evenNumbers = numbers.filter { it % 2 == 0 } // Output: [2, 4]
```

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> evenNumbers = numbers.stream()
                                   .filter(n -> n % 2 == 0)
                                   .collect(Collectors.toList()); // Output: [2, 4]
```

**Null Safety.**

```kotlin
var name: String = "John" // Non-nullable string
// name = null // Compilation error: Null cannot be a value of a non-null type String
```

```java
String name = "John";
// name = null; // Valid in Java
```


**Smart casting.**

```kotlin
fun printStringLength(text: Any) {
    if (text is String) {
        println("The length of the string is: ${text.length}") // No need for explicit casting
    }
}

printStringLength("Hello, Kotlin!") // Output: "The length of the string is: 14"
```

```java
void printStringLength(Object text) {
    if (text instanceof String) {
        String str = (String) text; // Explicit casting required
        System.out.println("The length of the string is: " + str.length());
    }
}

printStringLength("Hello, Java!"); // Output: "The length of the string is: 12"
```

**Corutine in limbaj.**
```kotlin
fun main() = runBlocking {
    launch {
        delay(1000L)
        println("Sarcină în corutină: Salut din corutină!")
    }
    println("Sarcină în main: Aștept...")
    delay(2000L)
}
```

```java
public static void main(String[] args) throws InterruptedException {
    Thread thread = new Thread(() -> {
        try {
            Thread.sleep(1000);
            System.out.println("Sarcină în thread: Salut din thread!");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    });
    thread.start();
    System.out.println("Sarcină în main: Aștept...");
    Thread.sleep(2000);
}
```

> Comutarea între corutine este mai rapidă decât comutarea între thread-uri, deoarece nu implică o comutare de context la nivel de sistem de operare.
