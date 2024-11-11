# Control Flow: Loops, Branching, and Control Transfer Statements

Control flow is fundamental to managing the logic of a program. Swift provides several types of control flow statements, including loop statements, branching statements, and control transfer statements. In this guide, we'll explore these control flow concepts with examples.

## Loop Statements
Loop statements allow you to execute a block of code repeatedly.

### For-In Loop

The `for-in` loop is used to iterate over collections, ranges, or sequences.

#### Examples:

```swift
let names = ["Alice", "Bob", "Charlie"]

for name in names {
    print("Hello, \(name)!")
}
// Output:
// Hello, Alice!
// Hello, Bob!
// Hello, Charlie!

for number in 1...5 {
    print(number)
}
// Output: 1, 2, 3, 4, 5
```

### While Loop

The `while` loop repeats a block of code as long as a specified condition remains true. It is particularly useful when the number of iterations is not known beforehand.

#### Example:

```swift
var counter = 3

while counter > 0 {
    print("Countdown: \(counter)")
    counter -= 1
}
// Output:
// Countdown: 3
// Countdown: 2
// Countdown: 1
```

### Repeat-While Loop

The `repeat-while` loop is similar to the `while` loop, except the condition is checked after each iteration, ensuring that the loop body is executed at least once.

#### Example:

```swift
var number = 0

repeat {
    print("Number is: \(number)")
    number += 1
} while number < 3
// Output:
// Number is: 0
// Number is: 1
// Number is: 2
```

## Branching Statements
Branching statements allow you to execute different blocks of code based on conditions.

### If Statement

The `if` statement is used to execute a block of code when a condition is true.

#### Example:

```swift
let score = 85

if score >= 90 {
    print("Excellent!")
} else if score >= 70 {
    print("Good job!")
} else {
    print("Keep trying!")
}
// Output: Good job!
```

### Guard Statement

The `guard` statement is used to exit a scope early when a certain condition is not met. It’s commonly used for input validation.

#### Example:

```swift
func greet(person: String?) {
    guard let name = person else {
        print("No name provided.")
        return
    }
    print("Hello, \(name)!")
}

greet(person: "Alice")   // Output: Hello, Alice!
greet(person: nil)        // Output: No name provided.
```

### Switch Statement

The `switch` statement is used to execute one of several possible blocks of code based on the value of an expression. It supports pattern matching and is more powerful than a simple `if-else` chain.

#### Example:

```swift
let fruit = "apple"

switch fruit {
case "apple":
    print("It’s an apple!")
case "banana":
    print("It’s a banana!")
case "orange":
    print("It’s an orange!")
default:
    print("Unknown fruit")
}
// Output: It’s an apple!
```

### Fallthrough in Switch

By default, Swift does not fall through to the next case in a `switch` statement, unlike some other programming languages. However, you can use the `fallthrough` keyword if you want this behavior.

#### Example:

```swift
let number = 3

switch number {
case 3:
    print("Three")
    fallthrough
case 4:
    print("Four")
default:
    print("Other number")
}
// Output:
// Three
// Four
```

## Control Transfer Statements
Control transfer statements are used to change the flow of execution within loops or other control structures.

### Break

The `break` statement is used to terminate the current loop or switch statement.

#### Example:

```swift
for i in 1...5 {
    if i == 3 {
        break
    }
    print(i)
}
// Output: 1, 2
```

### Continue

The `continue` statement is used to skip the current iteration of the loop and move to the next iteration.

#### Example:

```swift
for i in 1...5 {
    if i == 3 {
        continue
    }
    print(i)
}
// Output: 1, 2, 4, 5
```

### Return

The `return` statement is used to exit a function and optionally return a value.

#### Example:

```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

let result = add(3, 4)
print(result)   // Output: 7
```

## Labels

Swift also allows you to label loops and control flow statements, allowing you to `break` or `continue` a specific outer loop.

#### Example:

```swift
outerLoop: for i in 1...3 {
    for j in 1...3 {
        if j == 2 {
            continue outerLoop
        }
        print("i: \(i), j: \(j)")
    }
}
// Output:
// i: 1, j: 1
// i: 2, j: 1
// i: 3, j: 1
```

## Summary

- **Loop Statements**: Use `for-in`, `while`, and `repeat-while` to iterate over elements or execute code repeatedly.
- **Branching Statements**: Use `if`, `guard`, and `switch` to conditionally execute code.
- **Control Transfer Statements**: Use `break`, `continue`, `return`, and `fallthrough` to manage flow within loops and conditionals.

Swift’s control flow statements provide flexibility and power to effectively manage program logic, making code more expressive and readable.

## References

For more details, you can refer to the official Swift documentation:

- [Swift Language Guide - Control Flow](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html)
- [Swift Standard Library Reference](https://developer.apple.com/documentation/swift)

These references provide further insights and more advanced use cases for control flow in Swift.

