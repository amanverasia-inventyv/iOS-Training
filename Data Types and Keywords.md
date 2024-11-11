# Data Types and Keywords

This note covers the fundamental data types and keywords in the Swift programming language. We'll delve into data types such as `Int`, `UInt`, `Float`, `Double`, `Bool`, `String`, `Character`, `Optional`, and `Tuples`. We'll also explore essential keywords like `let`, `var`, `open`, `class`, and more.

---

## Data Types

Swift is a strongly-typed language, meaning every variable has a specific type that cannot change. Understanding data types is crucial for effective Swift programming.

### Int

The `Int` type represents a signed integer value. The size of `Int` depends on the platform:

- **On 32-bit platforms**: `Int` is 32 bits, storing values from `-2,147,483,648` to `2,147,483,647`.
- **On 64-bit platforms**: `Int` is 64 bits, storing values from `-9,223,372,036,854,775,808` to `9,223,372,036,854,775,807`.

```swift
let age: Int = 25
var count = 10  // Inferred as Int
```

#### Fixed-Size Integers

Swift also provides fixed-size integer types:

- `Int8`, `Int16`, `Int32`, `Int64`

```swift
let smallNumber: Int8 = 127
```

### UInt

The `UInt` type represents an unsigned integer, which can only store non-negative values. Like `Int`, its size depends on the platform:

- **On 32-bit platforms**: `UInt` is 32 bits, storing values from `0` to `4,294,967,295`.
- **On 64-bit platforms**: `UInt` is 64 bits, storing values from `0` to `18,446,744,073,709,551,615`.

```swift
let numberOfItems: UInt = 42
```

#### Fixed-Size Unsigned Integers

Fixed-size unsigned integers are also available:

- `UInt8`, `UInt16`, `UInt32`, `UInt64`

```swift
let byteValue: UInt8 = 255
```

### Float

`Float` is a 32-bit floating-point number, suitable for precision up to 6 decimal digits. It's used when memory is a constraint, and precision requirements are moderate.

```swift
let pi: Float = 3.141592
```

### Double

`Double` is a 64-bit floating-point number, providing precision up to 15 decimal digits. It's the default floating-point type in Swift.

```swift
let precisePi: Double = 3.141592653589793
```

### Bool

`Bool` represents a Boolean value, which can be either `true` or `false`. It's commonly used in conditional statements and control flow.

```swift
let isUserLoggedIn: Bool = true

if isUserLoggedIn {
    print("Welcome back!")
} else {
    print("Please log in.")
}
```

### String

`String` is a collection of characters used to represent text. Swift's `String` type is Unicode-compliant and supports international characters.

```swift
let greeting: String = "Hello, World!"
var name = "Alice"  // Inferred as String

// String interpolation
print("Welcome, \(name)!")
```

#### Multiline Strings

```swift
let multilineString = """
This is a
multiline string.
"""
```

### Character

`Character` represents a single character. It can store any single Unicode scalar value.

```swift
let exclamationMark: Character = "!"
```

Iterating over characters in a string:

```swift
for character in "Swift" {
    print(character)
}
```

### Optional

Optionals indicate that a variable might contain `nil`, meaning no value. This is particularly useful in scenarios where a value may be absent.

```swift
var middleName: String? = nil
middleName = "James"

// Unwrapping an optional using if-let
if let name = middleName {
    print("Middle name is \(name)")
} else {
    print("No middle name")
}

// Forced unwrapping (use with caution)
print(middleName!)  // Unsafe if middleName is nil

// Optional chaining
let uppercasedMiddleName = middleName?.uppercased()
```

#### Implicitly Unwrapped Optionals

Sometimes, an optional will always have a value after it's set once, in which case you can use an implicitly unwrapped optional.

```swift
var assumedString: String! = "An implicitly unwrapped optional string."
print(assumedString)  // No need to unwrap
```

### Tuples

Tuples group multiple values into a single compound value. The values can be of any type and don't have to be of the same type.

```swift
let httpError = (404, "Not Found")

// Decomposing a tuple
let (statusCode, statusMessage) = httpError
print("Status code: \(statusCode)")
print("Status message: \(statusMessage)")

// Accessing tuple elements by index
print("Error \(httpError.0): \(httpError.1)")

// Named tuple elements
let httpSuccess = (code: 200, message: "OK")
print("Status code: \(httpSuccess.code)")
print("Status message: \(httpSuccess.message)")
```

---

## Keywords

Swift has a set of reserved keywords that have special meanings. They are used to define variables, constants, functions, classes, and control flow.

### `let`

Use `let` to declare a constant, a value that cannot be changed once assigned. Constants are safer and convey intent more clearly.

```swift
let maximumNumberOfLoginAttempts = 5
// maximumNumberOfLoginAttempts = 10 // Error: Cannot assign to 'let' constant
```

### `var`

Use `var` to declare a variable whose value can be modified after it's set.

```swift
var currentLoginAttempt = 0
currentLoginAttempt += 1
```

### Other Keywords

#### `func`

Defines a function.

```swift
func greet(person: String) -> String {
    return "Hello, \(person)!"
}

print(greet(person: "Bob"))
```

#### `if`, `else`

Used for conditional execution.

```swift
if age >= 18 {
    print("You are an adult.")
} else {
    print("You are a minor.")
}
```

#### `for`, `while`

Used for loops.

```swift
for index in 1...5 {
    print("Index is \(index)")
}

var countdown = 5
while countdown > 0 {
    print("Countdown: \(countdown)")
    countdown -= 1
}
```

#### `switch`

Provides multiple possible execution paths.

```swift
let score = 85

switch score {
case 90...100:
    print("Grade: A")
case 80..<90:
    print("Grade: B")
case 70..<80:
    print("Grade: C")
default:
    print("Grade: F")
}
```

---

## Conclusion

Understanding Swift's basic data types and keywords is essential for building robust and efficient applications. This guide serves as a foundation to familiarize yourself with the syntax and fundamental concepts in Swift programming. By mastering these basics, you'll be well-equipped to delve deeper into more advanced topics.

---

**References:**

- [The Swift Programming Language (Swift 5.7)](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)

---

## Questions
### Data Types
1. What’s the difference between `Int` and `UInt` in Swift?
2. What would happen if you tried to assign a negative value to a `UInt` variable?
3. How does Swift handle the size of `Int` on 32-bit vs. 64-bit platforms?
4. Why might you choose a `Float` instead of a `Double` in Swift?
5. What’s the maximum precision of a `Float` in Swift?
6. What type of values does a `Bool` represent?
7. How is a `Character` different from a `String` in Swift?
8. What is an optional in Swift, and why is it useful?
9. How would you safely unwrap an optional to avoid runtime errors?

### Keywords
1. What is the main difference between `let` and `var`?
2. Why might you prefer to use `let` instead of `var`?
3. What does the `func` keyword do in Swift?
4. What keyword would you use to check for a condition in Swift?
5. What is the purpose of a `for` loop?
6. When would you use a `while` loop instead of a `for` loop?
7. What does a `switch` statement do in Swift?
8. How does a `switch` statement differ from an `if-else` chain in Swift?

### Gauging Understanding
1. What is the purpose of optional chaining?
2. How would you use optional chaining to access a property that might be `nil`?
3. What is type inference, and how does Swift use it?
4. What is the risk of using forced unwrapping on an optional?
5. How would you create a constant in Swift?
6. How would you create a variable in Swift?
7. What is the syntax to declare a multiline string in Swift?