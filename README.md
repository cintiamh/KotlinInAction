# KotlinInAction

## Kotlin: what and why

Simple Example
```kotlin
data class Person(val name: String, val age: Int? = null)

fun main(args: Array<String>) {
    val persons = listOf<Person>(Person("Alice"), Person("Bob", age = 29))
    val oldest = persons.maxBy { it.age ?: 0 }
    println("The oldest is: $oldest")
}
```

### Kotlin Primary Traits

#### Target platforms: server-side, Android, anywhere Java runs

Most common uses for Kotlin:
* Server side code (web)
* Android

Kotlin can be compiled into Java and JavaScript.

#### Statically typed

Type inference => the ability of the compiler to determine types from context.

Benefits of static typing:
* Performance
* Reliability
* Maintainability
* Tool support

#### Functional and object-oriented

Key concepts of functional programming:

* First-class functions
* Immutability
* No side effects

Benefits of functional: concise code.

Lambda expressions = anonymous functions

Another benefit: multithreading.
* because immutability, pure functions, you guarantee data consistency.

Testing is easier = defined input gives defined output.

Kotlin features for functional programming:
* Function types - allows to receive function as parameters and return
* Lambda expressions - define blocks of code with minimum boilerplate.
* Data classes - concise syntax for creating immutable value objects.
* APIs and standards to work with Objects and Collections using functional style.

With Kotlin you can use both object-oriented and functional programming where necessary.

### Kotlin applications

#### Kotlin on the server side

Works just like Java

* Web applications that return HTML pages to a browser
* Backends of mobile applications that expose a JSON API over HTTP
* Microservices that communicate with other microservices over an RPC protocol

#### Kotlin on Android

* The Anko library (https://github.com/kotlin/anko)
* Application reliability. Kotlin's type system, with its precise tracking of `null` values.
* Kotlin is compatible with Java 6

The code generated by Kotlin compiler is executed as efficiently as regular Java code.

### The Philosophy of Kotlin

#### Pragmatic

Kotlin is a practical language designed to solve real-world problems.

Another aspect of Kotlin's pragmatism is its focus on tooling. The IntelliJ IDEA plug-in was developed in lockstep with 
the compiler, and language features were always designed with tooling in mind.

#### Concise

Kotlin has a rich standard library that lets you replace long, repetitive sections of code with library method calls.

Kotlin's support for lambdas makes it easy to pass small blocks of code to library functions. This helps to encapsulate
all the common parts in the library and keep only the unique, task-specific portion in the user code.

Cocise code:
* less time to write
* less time to read.

#### Safe 

* Type safety with type inference
* Error check in compile time.
* Remove `NullPointerException`
* Avoid `ClassCastException`

```kotlin
// may be null
val s: String? = null
// may NOT be null
val s2: String = ""
```

#### Interoperable

You can work on Kotlin with Java and vice-versa. Kotlin uses existing Java frameworks.

### Using the Kotlin tools

#### Compiling Kotlin code

Kotlin source code file extension is `.kt`.

The Kotlin compiler generates a `.class` file.

The generated `.class` files are then packaged and executed using the standard procedure for the type application you're working on.

You can use the `kotlinc` command to compile your code.

Code compiled with Kotlin compiler depends on the **Kotlin runtime library**.

## Kotlin Basics 

### Basic elements: functions and variables

Encorages immutable data.

#### Hello, World!

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

* `fun` => declare function
* The parameter type is after the name.
* The function can be at the top level, it doesn't need to be in a class.
* Arrays are just classes
* You don't need to declare `System.out.println`.
* You can omit the semicolon at the end.

#### Functions

```kotlin
fun max(a: Int, b: Int): Int {
    return if (a > b) a else b
}
```

##### Statements and expressions

* Expression - has a value, which can be used as part of another expression.
* Statement - is always a top-level element in its enclosing block and doesn't have its own value.

Simplify even more:

```kotlin
fun max(a: Int, b:Int): Int = if (a > b) a else b
```

* **block body** - function with body between curly braces
* **expression body** - function returns and expression directly

Simplify even more:
```kotlin
fun max(a: Int, b: Int) = if (a > b) a else b
```

* **type inference** for expression body functions, the compiler can analyze the expression used as the body of the 
function and use its type as the function return type.

Note that for block body functions you need to explicitly define the return type.

#### Variables