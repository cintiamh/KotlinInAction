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