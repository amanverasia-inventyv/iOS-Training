# Collection Types in Swift: Array, Set, Dictionary

Swift provides three primary collection types: Arrays, Sets, and Dictionaries. These collection types are used to store values in an organized way, making it easier to manage and manipulate groups of related data.

## Arrays

An **array** is an ordered collection of values. Arrays in Swift can store values of the same type and can be mutable (using `var`) or immutable (using `let`).

### Creating Arrays

You can create an empty array or initialize an array with default values.

### Examples:

```swift
var emptyArray: [Int] = []          // Empty array of integers
var arrayOfStrings = ["Apple", "Banana", "Cherry"]
let repeatedArray = Array(repeating: 0, count: 5) // [0, 0, 0, 0, 0]
```

Swift infers the type of the array from the values provided, but you can also explicitly specify the type.

### Accessing and Modifying Arrays

You can access elements of an array using index values, starting from `0`. Arrays can also be modified by adding or removing elements.

### Examples:

```swift
var numbers = [1, 2, 3, 4, 5]

// Access elements
print(numbers[0])   // 1

// Modify elements
numbers[1] = 20
print(numbers)   // [1, 20, 3, 4, 5]

// Append elements
numbers.append(6)   // [1, 20, 3, 4, 5, 6]

// Insert elements
numbers.insert(10, at: 2)  // [1, 20, 10, 3, 4, 5, 6]

// Remove elements
numbers.remove(at: 4)  // [1, 20, 10, 3, 5, 6]
```

### Iterating Over an Array

You can iterate over an array using a `for-in` loop.

```swift
for fruit in arrayOfStrings {
    print(fruit)
}
// Output:
// Apple
// Banana
// Cherry
```

### Array Properties and Methods

- `count`: Returns the number of elements in the array.
- `isEmpty`: Returns `true` if the array is empty.
- `first` and `last`: Get the first or last element of the array.

### Examples:

```swift
print(numbers.count)    // 6
print(numbers.isEmpty)  // false
print(numbers.first)    // Optional(1)
print(numbers.last)     // Optional(6)
```

## Sets

A **set** is an unordered collection of unique values. Sets are particularly useful when you need to ensure that there are no duplicate elements.

### Creating Sets

You create a set by using an array literal. The type must be explicitly declared because a set does not maintain the order of elements.

### Examples:

```swift
var uniqueNumbers: Set<Int> = [1, 2, 3, 4, 5]
let fruits: Set = ["Apple", "Banana", "Cherry"]
```

### Adding and Removing Elements

Sets provide methods to add or remove elements.

```swift
uniqueNumbers.insert(6)  // {1, 2, 3, 4, 5, 6}
uniqueNumbers.remove(3)  // {1, 2, 4, 5, 6}
```

### Set Operations

Sets support various mathematical operations like union, intersection, and subtraction.

- `union(_:)`: Returns a new set containing all elements from both sets.
- `intersection(_:)`: Returns a new set with only the elements common to both sets.
- `subtracting(_:)`: Returns a new set with elements that are not in the specified set.

### Examples:

```swift
let setA: Set = [1, 2, 3, 4]
let setB: Set = [3, 4, 5, 6]

let unionSet = setA.union(setB)           // {1, 2, 3, 4, 5, 6}
let intersectionSet = setA.intersection(setB)  // {3, 4}
let subtractingSet = setA.subtracting(setB)    // {1, 2}
```

### Set Properties

- `isEmpty`: Checks if the set is empty.
- `count`: Returns the number of elements.

```swift
print(fruits.isEmpty)  // false
print(fruits.count)    // 3
```

## Dictionaries

A **dictionary** is an unordered collection of key-value pairs. Each key in a dictionary is unique, and it maps to a specific value.

### Creating Dictionaries

You can create a dictionary using a dictionary literal.

### Examples:

```swift
var countryCodes: [String: String] = [
    "US": "United States",
    "CA": "Canada",
    "FR": "France"
]
```

### Accessing and Modifying Dictionaries

You can access and modify dictionaries by using the key.

```swift
// Access value
if let country = countryCodes["CA"] {
    print(country)   // "Canada"
}

// Add or update value
countryCodes["GB"] = "United Kingdom"
print(countryCodes)  // ["US": "United States", "CA": "Canada", "FR": "France", "GB": "United Kingdom"]

// Remove a key-value pair
countryCodes["FR"] = nil
print(countryCodes)  // ["US": "United States", "CA": "Canada", "GB": "United Kingdom"]
```

### Iterating Over a Dictionary

You can iterate over a dictionary to get each key-value pair.

```swift
for (code, country) in countryCodes {
    print("\(code): \(country)")
}
// Output:
// US: United States
// CA: Canada
// GB: United Kingdom
```

### Dictionary Properties and Methods

- `count`: Returns the number of key-value pairs in the dictionary.
- `isEmpty`: Returns `true` if the dictionary is empty.
- `keys` and `values`: Properties to access all keys or values in the dictionary.

### Examples:

```swift
print(countryCodes.count)    // 3
print(countryCodes.isEmpty)  // false
print(countryCodes.keys)     // ["US", "CA", "GB"]
print(countryCodes.values)   // ["United States", "Canada", "United Kingdom"]
```

## References

For more details, you can refer to the official Swift documentation:

- [Swift Language Guide - Collection Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html)
- [Swift Standard Library Reference](https://developer.apple.com/documentation/swift)

These references provide further insights and more advanced use cases for collection types in Swift.
