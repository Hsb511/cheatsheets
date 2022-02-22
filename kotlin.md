# Kotlin

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
| ref \ returns | receiver  | lambda         |
|---------------|-----------|----------------|
| it            |  **also** |     **let**    |
| this          | **apply** | **run / with** |

## Null Safety on String or Collections

```kotlin
ifEmpty { }         // if the receiver is null or empty change its value
ifBlank { }         // if the receiver is null or empty or blank change its value
orEmpty()           // returns an empty value (String or Collection) if null or the value itself otherwise
```

## Collections

### Collection literals

```kotlin
listOf()            // returns an immutable list containing the paramaters
mutableListOf()     // returns a mutable list containing the parameters
setOf()             // returns a set containing the parameters
setOfNotNull()      // returns a set containing the non null parameters
arrayOf()           // returns an array containing the parameters
asSequence()        // Creates a Sequence instance that wraps the original array returning its elements when being iterated.
```

### Collection processing

```kotlin
.forEach {}             // Performs the given action on each element
.filter {}              // Returns a list containing only elements matching the given predicate.
.filterNotNull()        // Returns a list containing only the non null elements
.filterIsInstance<>()   // Returns a list containing only the elements with given type
.map {}                 // Returns elements after a transformation
.flatMap {}             // Returns a single list of all elements yielded from results of transform function
.reduce {}              // Accumulates value starting with the first element and applying operation from left to right
.fold {}                // Accumulates value starting with initial value and applying operation from left to right 
.sortedBy {}            // Returns a list of all elements sorted according to natural sort order of the value returned by specified selector function.
.sortedWith()           // Returns a list of all elements sorted according to the specified comparator
.groupBy {}             // Groups elements by the key returned by the given keySelector function applied to each element 
.distinct()             // Returns a list containing only unique elements from the given array.
```

### Retrieve Collection parts

```kotlin
.any {}                 
.none {}
.first {}
.firstOrNull {}
.take()                 // Returns a list of the n first elements of the collection
.takeLast()             // Returns a list of the n last elements of the collection
.minOf {}
.maxOf {}
.count()
.average()              // Returns an average value of elements in the array.
.sum()
```
