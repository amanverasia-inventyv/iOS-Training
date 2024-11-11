# Higher Order Functions: Map, FlatMap, CompactMap, Reduce, Sort

Swift provides several powerful **higher-order functions** that allow you to manipulate collections in a more expressive and concise way. The most common ones include `map`, `flatMap`, `compactMap`, `reduce`, and `sort`. Let's take an in-depth look at each of these functions, with examples to understand how they work.

## Map

The `map` function is used to transform each element in a collection and return a new collection containing the transformed values. It applies the provided closure to each element in the collection.

### Example:

```swift
let numbers = [1, 2, 3, 4, 5]
let squares = numbers.map { $0 * $0 }
print(squares)   // [1, 4, 9, 16, 25]

let names = ["Alice", "Bob", "Charlie"]
let uppercaseNames = names.map { $0.uppercased() }
print(uppercaseNames)   // ["ALICE", "BOB", "CHARLIE"]
```

In the example above, `map` transforms each value in the `numbers` array to its square, resulting in an array of squares.

## FlatMap

The `flatMap` function is used to transform elements and flatten the resulting nested collections into a single array. This is useful when you have an array of arrays, and you want a single array with all the elements.

### Example:

```swift
let nestedArray = [[1, 2, 3], [4, 5], [6, 7, 8]]
let flattenedArray = nestedArray.flatMap { $0 }
print(flattenedArray)   // [1, 2, 3, 4, 5, 6, 7, 8]
```

In this example, `flatMap` flattens the nested array into a single array.

## CompactMap

The `compactMap` function is used to transform a collection and remove any `nil` values in the process. It performs the transformation and unwraps the resulting optional values, excluding the `nil` results.

### Example:

```swift
let numbersWithNil: [Int?] = [1, nil, 3, nil, 5]
let nonNilNumbers = numbersWithNil.compactMap { $0 }
print(nonNilNumbers)   // [1, 3, 5]

let stringNumbers = ["1", "two", "3", "four"]
let validNumbers = stringNumbers.compactMap { Int($0) }
print(validNumbers)    // [1, 3]
```

In the example above, `compactMap` removes any `nil` values from the array while transforming elements.

## Reduce

The `reduce` function is used to combine all elements in a collection into a single value, by repeatedly applying the provided closure. It takes an initial value and a closure that processes each element in the collection.

### Example:

```swift
let numbers = [1, 2, 3, 4, 5]
let sum = numbers.reduce(0) { $0 + $1 }
print(sum)   // 15

let words = ["Swift", "is", "awesome"]
let sentence = words.reduce("", { $0 + " " + $1 }).trimmingCharacters(in: .whitespaces)
print(sentence)   // "Swift is awesome"
```

In the first example, `reduce` calculates the sum of the elements in the `numbers` array, starting with an initial value of `0`.

## Sort

The `sort` and `sorted` functions are used to arrange the elements of a collection in a specific order. The `sort` function sorts the collection in-place, while `sorted` returns a new sorted collection.

### Examples:

```swift
var numbers = [5, 2, 8, 3, 1]
numbers.sort()
print(numbers)   // [1, 2, 3, 5, 8]

let names = ["Charlie", "Alice", "Bob"]
let sortedNames = names.sorted(by: <)
print(sortedNames)   // ["Alice", "Bob", "Charlie"]
```

In the examples above, `sort` is used to modify the original array, while `sorted(by:)` is used to create a new sorted version of the array.

### Custom Sort

You can provide a custom closure to determine how the elements should be sorted.

```swift
let descendingNumbers = numbers.sorted { $0 > $1 }
print(descendingNumbers)   // [8, 5, 3, 2, 1]
```

Here, `sorted` sorts the elements in descending order using a custom closure.

## Summary

- **`map`**: Transforms each element in the collection.
- **`flatMap`**: Transforms and flattens nested collections.
- **`compactMap`**: Transforms the collection while removing `nil` values.
- **`reduce`**: Combines all elements into a single value.
- **`sort`/`sorted`**: Sorts the elements of a collection.

These higher-order functions make code more expressive and concise, making it easier to work with collections in Swift.

## References

For more details, you can refer to the official Swift documentation:

- [Swift Language Guide - Closures](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)
- [Swift Standard Library Reference](https://developer.apple.com/documentation/swift)

These references provide further insights and more advanced use cases for higher-order functions in Swift.

