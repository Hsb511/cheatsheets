# Kotlin

## Null Safety

```kotlin
ifBlank { }
ifEmpty { }
orEmpty()
```

## Collections

### Collection literals

```kotlin
listOf()
mutableListOf()
setOf()
setOfNotNull()
arrayOf()
asSequence()
```

### Collection processing

```kotlin
.forEach {}
.filter {}
.filterNotNull()
.filterIsInstance<>()
.map {}
```

### Collection result

```kotlin
.any {}
.none {}
.first {}
.minOf {}
.maxOf {}
```

## Scope functions

```kotlin
// let : can be used for executing a code block only with non-null values
val length = str?.let { it.length }

// let : can be used to invoke one or more functions on results of call chains.
val numbers = mutableListOf("one", "two", "three", "four", "five")
numbers.map { it.length }.filter { it > 3 }.let(::println) 

// with : can be used for calling functions on the context object without providing lambda result
val numbers = mutableListOf("one", "two", "three")
val firstAndLast = with(numbers) {
    "The first element is ${first()}, the last element is ${last()}"
}

// run : object configuration and computing result 
val service = MultiportService("https://example.kotlinlang.org", 80)
val result = service.run {
    port = 8080
    query(prepareRequest() + " to port $port")
}

// apply : object configuration : set values to the object attributes
rights.apply { 
    access = 0
    expired = true
}

// also : for actions that need a reference to the object rather than its properties and functions, 
// or when you don't want to shadow this reference from an outer scope
fun UserEntity.toDto() = UserDto().also {
    it.firstname = firstname
    it.lastname = lastname
}
```
