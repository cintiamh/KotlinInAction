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

