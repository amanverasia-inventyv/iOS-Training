# Operators 

Swift provides a wide range of operators that make coding convenient and expressive. These include arithmetic operators, comparison operators, logical operators, assignment operators, and more. Let’s dive into the various types of operators available in Swift with plenty of examples to make things clear.

## Arithmetic Operators

Arithmetic operators are used to perform basic mathematical operations.

- `+` : Addition
- `-` : Subtraction
- `*` : Multiplication
- `/` : Division
- `%` : Remainder (Modulo)

### Examples:

```swift
let a = 10
let b = 3

let sum = a + b          // 13
let difference = a - b   // 7
let product = a * b      // 30
let quotient = a / b     // 3 (integer division)
let remainder = a % b    // 1
```

Swift uses standard operator precedence rules to evaluate expressions, so multiplication and division are performed before addition and subtraction.

```swift
let result = 2 + 3 * 4   // 14 because 3 * 4 is evaluated first
```

## Compound Assignment Operators

Compound assignment operators combine an operation with assignment in one step. They are shortcuts that make code easier to read.

- `+=` : Addition assignment
- `-=` : Subtraction assignment
- `*=` : Multiplication assignment
- `/=` : Division assignment

### Examples:

```swift
var c = 5
c += 3   // c = 8
c -= 2   // c = 6
c *= 4   // c = 24
c /= 3   // c = 8
```

## Comparison Operators

Comparison operators are used to compare values, returning a Boolean value (`true` or `false`).

- `==` : Equal to
- `!=` : Not equal to
- `>`  : Greater than
- `<`  : Less than
- `>=` : Greater than or equal to
- `<=` : Less than or equal to

### Examples:

```swift
let x = 10
let y = 20

print(x == y)   // false
print(x != y)   // true
print(x < y)    // true
print(x >= 10)  // true
```

## Logical Operators

Logical operators are used to combine multiple Boolean expressions.

- `&&` : Logical AND
- `||` : Logical OR
- `!`  : Logical NOT

### Examples:

```swift
let isRaining = false
let isCold = true

// Logical AND
if isRaining && isCold {
    print("It’s raining and cold.")
} else {
    print("The weather is not both rainy and cold.")
}

// Logical OR
if isRaining || isCold {
    print("It’s either raining or cold.")
}

// Logical NOT
if !isRaining {
    print("It’s not raining.")
}
```

## Range Operators

Swift provides two kinds of range operators: closed range (`...`) and half-open range (`..<`).

- `a...b` : Closed Range. This creates a range from `a` to `b`, including both `a` and `b`.
- `a..<b` : Half-Open Range. This creates a range from `a` to `b`, excluding `b`.

### Examples:

```swift
// Closed range
for number in 1...5 {
    print(number)   // 1, 2, 3, 4, 5
}

// Half-open range
for number in 1..<5 {
    print(number)   // 1, 2, 3, 4
}
```

## Ternary Conditional Operator

The ternary conditional operator is a shorthand for simple `if-else` statements. It follows the format:

`condition ? expressionIfTrue : expressionIfFalse`

### Example:

```swift
let score = 85
let result = score >= 50 ? "Pass" : "Fail"
print(result)   // "Pass"
```

## Nil-Coalescing Operator

The nil-coalescing operator (`??`) unwraps an optional and provides a default value if the optional is `nil`.

### Example:

```swift
let userInput: String? = nil
let defaultValue = "Default"

let value = userInput ?? defaultValue
print(value)   // "Default"
```

## Assignment Operator

The assignment operator (`=`) is used to assign a value to a variable or constant.

### Example:

```swift
let name = "Alice"
var age = 30
age = 31
```

## Bitwise Operators

Bitwise operators manipulate individual bits in binary representations.

- `&` : AND
- `|` : OR
- `^` : XOR
- `~` : NOT
- `<<` : Left Shift
- `>>` : Right Shift

### Examples:

```swift
let bitwiseAnd = 6 & 3     // 2 (0110 & 0011 = 0010)
let bitwiseOr = 6 | 3      // 7 (0110 | 0011 = 0111)
let bitwiseXor = 6 ^ 3     // 5 (0110 ^ 0011 = 0101)
let bitwiseNot = ~6        // -7 (inverts all bits of 6)
let leftShift = 1 << 3     // 8 (0001 shifted left by 3 positions = 1000)
let rightShift = 8 >> 2    // 2 (1000 shifted right by 2 positions = 0010)
```

## Overflow Operators

Swift has special overflow operators for handling arithmetic operations that would exceed the bounds of the data type.

- `&+` : Overflow Addition
- `&-` : Overflow Subtraction
- `&*` : Overflow Multiplication

### Example:

```swift
var maxUInt8 = UInt8.max  // 255
let overflow = maxUInt8 &+ 1   // 0 (wraps around to the minimum value)
```

## References

For more details, you can refer to the official Swift documentation:

- [Swift Language Guide - Basic Operators](https://docs.swift.org/swift-book/LanguageGuide/BasicOperators.html)
- [Swift Standard Library Reference](https://developer.apple.com/documentation/swift)

These references provide further insights and more advanced use cases for operators in Swift.

