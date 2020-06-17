# KotlinInAction

1. [Kotlin: what and why](#kotlin-what-and-why)
2. [Kotlin Basics](#kotlin-basics)
3. [Defining and calling functions](#defining-and-calling-functions)

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

Kotlin allows to omit the type from many variable declarations.

There are two keywords to declare variables:
* **val** (from value) - immutable reference.
* **var** (from variable) - mutable reference. but type is fixed.

Prefere to declare as `val`.

```kotlin
val message: String
if (canPerformOperation()) {
    message = "Success"
}
else {
    message = "Failed"
}
```

#### Easier string formatting: string templates

```kotlin
fun main(args: Array<String>) {
    val name = if (args.size > 0) args[0] else "Kotlin"
    println("Hello, $name!")
}
```

More complex:
```kotlin
fun main(args: Array<String>) {
    println("Hello, ${if (args.size > 0) args[0] else "someone"}")
}
```

### Classes and Properties

**Value Objects** => Classes containing only data but no code

```kotlin
class Person(val name: String)
```

#### Properties

Java
* **accessor methods** getters and setters.
* **property** the combination of the field and its accessor.

In Kotlin you declare the property in a class the same way to declare a variable: with `val` and `var` keywords.

If the property name starts with `is`, no additional prefix is added.

```kotlin
println(person.isMarried)
``` 

#### Custom accessors

```kotlin
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
        get() {
            return height == width
        }
}
```

#### Kotlin source code layout: directories and packages

Like in Java, Kotlin has the concept of packages.
Every Kotlin file can have a `package` statement at the beginning.
If classes are inside the same package, they don't need to be imported.
Import statements are placed at the beginning of the file using the `import` keyword.

```kotlin
package geometry.shapes

import java.util.Random

class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
        get() {
            return height == width
        }
}

fun createRandomRectangle(): Rectangle {
    val random = Random()
    return Rectangle(random.nextInt(), random.nextInt())
}
```

Kotlin doesn't make any distinction between importing a class or a function.

Importing from another package
```kotlin
package geometry.example
import geometry.shape.createRadomRectangle

fun main(args: Array<String>) {
    println(createRandomRectangle().isSquare)
}
```

Kotlin allows to have multiple classes in a single file and choose any name for the file.
You can also use any directory structure for the file.

But it's a good idea to follow Java's package structure.
```
- geometry/
    - example/
        - Main
    - shapes/
        - Rectangle
        - RectangleUtil
```

### Representing and handling choices: enums and "when"

`when` => Java's `switch`

#### Declaring enum classes

```kotlin
enum class Color {
    RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET
}
```

Enums with properties:
```kotlin
enum class Color(val r: Int, val g: Int, val b: Int) {
    RED(255, 0, 0), ORANGE(255, 165, 0), YELLOW(255, 255, 0), GREEN(0, 255, 0),
    BLUE(0, 0, 255), INDIGO(75, 0, 130), VIOLET(238, 130, 238);

    fun rgb() = (r * 256 + g) * 256 + b
}
```

The semicolon separates the enum constant list from the method definitions.

#### Using "when" to deal with enum classes

`when` is an expression that returns a value, so you can write a function with an expression body, returning `when` 
expression directly.

```kotlin
fun getMnemonic(color: Color) =
    when (color) {
        Color.RED -> "Richard"
        Color.ORANGE -> "Of"
        Color.YELLOW -> "York"
        Color.GREEN -> "Gave"
        Color.BLUE -> "Battle"
        Color.INDIGO -> "In"
        Color.VIOLET -> "Vain"
    }

>>> println(getMnemonic(Color.BLUE))
Battle
```

You can also combine multiple values in the same branch if you separate them with commas.

```kotlin
fun getWarmth(color: Color) = 
    when(color) {
        Color.RED, Color.ORANGE, Color.YELLOW -> "warm"
        Color.GREEN -> "neutral"
        Color.BLUE, Color.INDIGO, Color.VIOLET -> "cold"
    }
```

You can import the constant values from enums:
```kotlin
import ch02.colors.Color
import ch02.colors.Color.*

fun getWarmth(color: Color) = 
    when(color) {
        RED, ORANGE, YELLOW -> "warm"
        GREEN -> "neutral"
        BLUE, INDIGO, VIOLET -> "cold"
    }
```

#### Using `when` with arbitrary objects

`when` allows any objects.

```kotlin
fun mix(c1: Color, c2: Color) =
    when (setOf(c1, c2)) {
        setOf(RED, YELLOW) -> ORANGE
        setOf(YELLOW, BLUE) -> GREEN
        setOf(BLUE, VIOLET) -> INDIGO
        else -> throw Exception("Dirty color")
    }
```

`setOf` => creates a `Set`. A `set` is a collection for which the order of items doesn't matter.

#### Using `when` without an argument 

Instantiate `Set` for all possibilities all the time could get innefficient. A more efficient way to implement is:

```kotlin
fun mixOptimized(c1: Color, c2: Color) =
    when {
        (c1 == RED && c2 == YELLOW) || (c1 == YELLOW && c2 == RED) -> ORANGE
        (c1 == YELLOW && c2 == BLUE) || (c1 == BLUE && c2 == YELLOW) -> GREEN
        (c1 == BLUE && c2 == VIOLET) || (c1 == VIOLET && c2 == BLUE) -> INDIGO
        else -> throw Exception("Dirty color")
    }
```

#### Smart casts: combining type checks and casts

```kotlin
interface Expr
class Num(val value: Int) : Expr
class Sum(val left: Expr, val right: Expr) : Expr

>>> println (eval(Sum(Shum(Num(1), Num(2)), Num(4))))
```

In Kotlin, you check type using `is` check.

`smart cast` => The compiler performs the cast for you.

#### Refactoring: replacing "if" with "when"

In Kotlin, there is no ternary operator because, unlike in Java, the `if` expression returns a value.

```kotlin
fun eval(e: Expr): Int =
    if (e is Num) {
        e.value
    } else if (e is Sum) {
        eval(e.right) + eval(e.left)
    } else {
        throw IllegalArgumentException("Unknown expression")
    }
``` 

Rewriting with `when`
```kotlin
fun eval(e: Expr): Int =
    when (e) {
        is Num -> e.value
        is Sum -> eval(e.right) + eval(e.left)
        else -> throw IllegalArgumentException("Unknown expression")
    }
```

#### Blocks as branches of "if" and "when"

```kotlin
fun evalWithLogging(e: Expr): Int =
    when(e) {
        is Num -> {
            println("num: ${e.value}")
            e.value
        }
        is Sum -> {
            val left = evalWithLogging(e.left)
            val right = evalWithLogging(e.right)
            println("sum: $left + $right")
            left + right
        }
        else -> throw IllegalArgumentException("Unknown expression")
    }
```

The last expression in a block is the result.

A function can have either an expression body that can't be a block or a block body with explicit `return` statement inside.

### Iterating over things: "while" and "for" loops

#### The "while" loop

Just like Java.

```kotlin
while (condition) {
    /* ... */
}

do {
    /* ... */
} while (condition)
```

#### Iterating over numbers: ranges and progressions

In Kotlin there's no regular Java `for` loop. Kotlin uses `ranges`.

```kotlin
val oneToTen = 1..10
```

Ranges in Kotlin are closed or inclusive. (the second value is part of the range.)

**progression** loop over all the values in a range.

```kotlin
fun fizzBuzz(i: Int) = when {
    i % 15 == 0 -> "FizzBuzz "
    i % 3 == 0 -> "Fizz "
    i % 5 == 0 -> "Buzz "
    else -> "$i "
}

fun main(args: Array<String>) {
    for (i in 1..100) {
        print(fizzBuzz(i))
    }

    for (i in 100 downTo 1 step 2) print(fizzBuzz(i))
}
```

#### Iterating over maps

```kotlin
package ch02

import java.util.*

fun main(args: Array<String>) {
    val binaryReps = TreeMap<Char, String>()

    for (c in 'A'..'F') {
        val binary = Integer.toBinaryString(c.toInt())
        binaryReps[c] = binary
    }

    for ((letter, binary) in binaryReps) {
        println("$letter = $binary")
    }
}
```

#### Using "in" to check collection and range membership

* `in` => value is in range.
* `!in` => value isn't in range.

```kotlin
fun isLetter(c: Char) = c in 'a'..'z' || c in 'A'..'Z'
fun isNotDigit(c: Char) = c !in '0'..'9'
```

If any class supports comparing instances by implementing `java.lang.Comparable`, you can create ranges of objects of that type.

### Exceptions in Kotlin

```kotlin
import java.lang.IllegalArgumentException

if (percentage !in 0..100) {
    throw  IllegalArgumentException("A percentage value must be between 0 and 100: $percentage")
}
```

You don't need to use `new` keyword to create an instance of the exception.

#### "try", "catch", and "finally"

```kotlin
fun readNumber(reader: BufferedReader): Int? {
    try {
        val line = reader.readLine()
        return Integer.parseInt(line)
    } catch (e: NumberFormatException) {
        return null
    } finally {
        reader.close()
    }
}
```

The `throws` clause isn't present in the code.

#### "try" as an expression

The `try` keyword in Kotlin introduces an expression, and you can assign its value to a variable.
Unlike with `if`, you always need to enclose the statement body in curly braces.

```kotlin
fun readNumber(reader: BufferedReader): Int? {
    val number = try { 
        Integer.parseInt(reader.readLine())
    } catch (e: NumberFormatException) {
        null
    }
    println(number)
}
```

## Defining and calling functions
