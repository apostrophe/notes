# Kotlin Basics

**Variables**
Variables are declared with a either the `val` (read-only) keyword, or `var` keyword.

And the type can be inferred or explicitly declared.

```kotlin
val immutable = "Cannot be reassigned" // Read-only (like final in Java)
var mutable = "Can be reassigned"      // Mutable variable

val inferredType = 42                  // Type inference
val explicitType: Int = 42             // Explicit type
```

**functions**
declared with the `fun` keyword
```kotlin
fun greet(name: String): String {
    return "Hello, $name"
}

// Single-expression function
fun add(a: Int, b: Int) = a + b

// Default parameters
fun greet(name: String = "World") = "Hello, $name"
```

**null safety**

```kotlin
var notNull: String = "Hello"
// notNull = null // Compile error

var nullable: String? = "Hello"
nullable = null  // OK

// Safe call operator
val length = nullable?.length

// Elvis operator
val length = nullable?.length ?: 0


// default is non-nullable
var someString = "a string"
someString = null // assigning variable to null results in compile-time error

var isItNullable: String? = null;
var len = isItNullable?.length;
println(len) // prints null -- so len is a nullable value
```

**data classes**

```kotlin
data class Person(val name: String, val age: Int)

val person = Person("Alice", 30)
println(person.name)  // Auto-generated getters
```

**control flow**

```kotlin
// If as an expression
val max = if (a > b) a else b

// Traditional 'if' statement
if (check) {
    d = 1
} else {
    d = 2
}

// When (like switch)
when (x) {
    1 -> println("One")
    2, 3 -> println("Two or Three")
    else -> println("Other")
}

var y: String? = when (x) {
    1 -> "One"
    2, 3 -> "Two or Three"
    else -> null
}

```

**loops: for, foreach, while, do**

```kotlin
for (i in 1..5) {
    println(i)  // 1, 2, 3, 4, 5
}

for (i in 1 until 5) {
    println(i)  // 1, 2, 3, 4
}

list.forEach { item ->
    println(item)
}
```

**classes**

```kotlin
// class declarations are simply the class keyword, the name of the class, 
// and a list of class fields as parameters
class Contact(val id: Int, var email: String)

fun main() {
    // initializing a class
    val contact = Contact(1, "mary@gmail.com")
    
    // accessing a member field/property
    println(contact.email)           

    // updating the value of the property: email
    contact.email = "jane@gmail.com"
    
    // Prints the new value of the property: email
    println(contact.email)           
    // jane@gmail.com
}
```

**inheritance**
```kotlin
// initialized
open class Animal(val name: String) {
    // member funtion
    open fun sound() = "Some sound"
}

// extending a class
class Dog(name: String) : Animal(name) {
    // member funtion
    override fun sound() = "Woof"
}

// 
```

**string templates**
analagous to string templates in typescript, using "" instead of ``

```kotlin
val name = "Alice"
val greeting = "Hello, $name"
val message = "Length: ${name.length}"
```

**collections**
only list, set and map?
```kotlin
val list = listOf(1, 2, 3)           // Immutable
val mutableList = mutableListOf(1, 2, 3)

val map = mapOf("a" to 1, "b" to 2)
val mutableMap = mutableMapOf("a" to 1)
```

**lambda expressions**

```kotlin
val square = { x: Int -> x * x }
println(square(5))  // 25

val numbers = listOf(1, 2, 3, 4)
val doubled = numbers.map { it * 2 }
```

**function type**
functions can be passed to other functions

```kotlin
```

**data classes**  
Data classes in Kotlin are special classes designed to hold data. They automatically generate useful methods like `equals()`, `hashCode()`, `toString()`, and `copy()`.

Example:
```kotlin
// declare a data class
data class User(val id: Int, val name: String, val email: String)

// initialize
val user1 = User(1, "Alice", "alice@example.com")
println(user1)  // User(id=1, name=Alice, email=alice@example.com)

val user2 = user1.copy(name = "Alicia")
println(user2)  // User(id=1, name=Alicia, email=alice@example.com)

val (id, name, email) = user1
println("ID: $id, Name: $name")  // ID: 1, Name: Alice
```

**destructuring is allowed**

```kotlin
val person = Person("Alice", 30)
val (name, age) = person  // Destructuring

println(name)  // Alice
println(age)   // 30
```

** **

```kotlin
```

** **

```kotlin
```

