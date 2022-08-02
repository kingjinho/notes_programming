# Builder Pattern

> Build up from small
>
> When it's ready, create an instance

- Separate instance creation procedure from its class

## Example: StringBuilder

```kotlin

fun appendString() {
    val sampleString = StringBuilder().apply {
        append("a")
        append("a")
        append("a")
        append("a")
        append("a")
        append("a")
    }.toString()
}
```

## Fluent interface

- These days, when implementing builder pattern, programming language supports this interface
- returns **itself**
    - May think that it violates OOP design, but now it's common practice.

```kotlin
fun appendString() {
    val sampleString = StringBuilder()
        .append("a")
        .append("a")
        .append("a")
        .append("a")
        .append("a")
        .append("a")
        .toString()
}
```

## Wrong Usage of Builder Pattern

```kotlin
class EmployeeBuilder(private val id: Int) {

    lateinit var age: Int
    lateinit var startingYear: Int
    lateinit var firstName: String
    lateinit var lastName: String

    fun withAge(age: Int): EmployeeBuilder {
        this.age = age
    }

    fun withStartingYear(startingYear: Int): EmployeeBuilder {
        this.startingYear = startingYear
    }

    fun withName(firstName: String, lastName: String): EmployeeBuilder {
        this.firstName = firstName
        this.lastName = lastName
    }

    fun build(): Employee {
        return Employee(id, age, startingYear, firstName, lastName)
    }
}
```

- This can lower the risk of creating an instance with wrong data
- `However, this solution can still make problem if client creates an object with wrong parameters`
    - or what if client misses calling one of `with* method`???
    - `Missing state? violates OOP principle!`
        - `An object has its valid states when it's created`

### Solution to this problem

- Create a class that contains empty constructor
    - setter to set states

```kotlin
class CreateEmployeeParams {

    lateinit var age: Int
    lateinit var startingYear: Int
    lateinit var firstName: String
    lateinit var lastName: String

    fun setAge(age: Int) {
        this.age = age
    }
    ...
}

class Employee(private val params: CreateEmployeeParams) {
    private val age: Int = params.age
    private val startingYear = params.startingYear
    ...
}
```   

- Still, if client forget to call one of setters...still cause an error
    - or, if new states has added
  
### Better Solution

- Named parameter!
- Defensive
- No need builder pattern
```kotlin
class Employee(val age: Int, val startingYear: Int, val firstName: String, val lastName: String) {
    
}

fun main() {
    val employee = Employee(age = 10, startingYear = 2020, firstName = "Jack", lastName = "Grealish")
}
```