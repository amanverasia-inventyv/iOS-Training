# Extensions in Swift

Extensions in Swift are a powerful feature that allows you to add new functionality to existing classes, structures, enumerations, and protocols. They enable you to extend types for which you do not have access to the original source code, such as types defined in the Swift Standard Library or in third-party libraries.

## What Are Extensions?

An extension adds new functionality to an existing type:

- **Computed Properties**: Add new computed properties.
- **Methods**: Add new instance and type methods.
- **Initializers**: Provide new initializers.
- **Subscripts**: Add new subscripts.
- **Nested Types**: Define and use new nested types.
- **Conform to Protocols**: Make an existing type conform to a protocol.

## Syntax

The basic syntax for an extension is:

```swift
extension SomeType {
    // New functionality to add to SomeType
}
```

## Adding Computed Properties

You can add computed instance and type properties to existing types.

### Example: Adding a Computed Property

```swift
extension Double {
    var km: Double { return self * 1_000.0 }
    var m:  Double { return self }
    var cm: Double { return self / 100.0 }
}

let distance = 5.0.km
print("Distance in meters: \(distance)") // Output: Distance in meters: 5000.0
```

In this example, we extend `Double` to add computed properties for unit conversions.

## Adding Methods

Extensions can add new instance and type methods to existing types.

### Example: Adding an Instance Method

```swift
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}

3.repetitions {
    print("Hello!")
}

// Output:
// Hello!
// Hello!
// Hello!
```

Here, we add a `repetitions` method to `Int` that executes a closure multiple times.

## Adding Mutating Instance Methods

When extending value types (structures and enumerations), you can add mutating instance methods.

### Example: Adding a Mutating Method

```swift
extension Int {
    mutating func square() {
        self = self * self
    }
}

var number = 5
number.square()
print(number) // Output: 25
```

The `square` method modifies the value of the integer it is called on.
(add an example of cube)


## Adding Initializers

Extensions can add new initializers to existing types.

### Example: Adding an Initializer

```swift
struct Size {
    var width = 0.0
    var height = 0.0
}

extension Size {
    init(side: Double) {
        self.width = side
        self.height = side
    }
}

let square = Size(side: 10.0)
print("Width: \(square.width), Height: \(square.height)") // Output: Width: 10.0, Height: 10.0
```

This extension adds a convenience initializer to the `Size` struct.

## Adding Subscripts

Extensions can add new subscripts to existing types.

### Example: Adding a Subscript

```swift
extension String {
    subscript(index: Int) -> Character {
        return self[self.index(self.startIndex, offsetBy: index)]
    }
}

let text = "Hello"
print(text[1]) // Output: e
```

This extension allows you to access characters in a string using integer indices.

## Adding Nested Types

Extensions can add new nested types to existing classes, structures, or enumerations.

### Example: Adding a Nested Enum

```swift
extension Int {
    enum Kind {
        case negative, zero, positive
    }

    var kind: Kind {
        switch self {
        case 0:
            return .zero
        case let x where x > 0:
            return .positive
        default:
            return .negative
        }
    }
}

let numberKind = (-5).kind
print(numberKind) // Output: negative
```

Here, we add a nested `Kind` enum to `Int` and a computed property to determine the kind of integer.

## Conforming to Protocols

Extensions can make existing types conform to protocols.

### Example: Conforming to a Protocol

```swift
protocol FullyNamed {
    var fullName: String { get }
}

struct Person {
    var firstName: String
    var lastName: String
}

extension Person: FullyNamed {
    var fullName: String {
        return "\(firstName) \(lastName)"
    }
}

let person = Person(firstName: "John", lastName: "Doe")
print(person.fullName) // Output: John Doe
```

In this example, we extend `Person` to conform to the `FullyNamed` protocol.

## Limitation: Stored Properties

Extensions cannot add stored properties or property observers to existing types.

```swift
// This will result in a compile-time error
extension Person {
    var age: Int = 0 // Error: Extensions may not contain stored properties
}
```

Extensions are limited to adding computed properties, methods, initializers, subscripts, and nested types.

## Using Extensions to Organize Code

Extensions can be used to organize code by functionality, especially in large projects.

### Example: Organizing by Protocol Conformance

```swift
class ViewController: UIViewController {
    // ViewController implementation
}

// MARK: - UITableViewDataSource
extension ViewController: UITableViewDataSource {
    // Data source methods
}

// MARK: - UITableViewDelegate
extension ViewController: UITableViewDelegate {
    // Delegate methods
}
```

### (Add another example here or simply it)

By using extensions, you can separate protocol conformances and keep your code organized.

## Extending Generic Types
### (add this in the generic file) [[generic]]
You can extend generic types and even add constraints.

### Example: Extending a Generic Type with Constraints

```swift
extension Array where Element: Equatable {
    func allEqual() -> Bool {
        guard let firstElement = self.first else { return true }
        return !self.contains { $0 != firstElement }
    }
}

let numbers = [1, 1, 1, 1]
print(numbers.allEqual()) // Output: true

let words = ["apple", "apple", "orange"]
print(words.allEqual()) // Output: false
```

In this example, we extend `Array` where the `Element` conforms to `Equatable` to add an `allEqual` method.

## Practical Use Cases

- **Adding Utility Functions**: Extend types to include utility methods relevant to your project.
- **Protocol Conformance**: Use extensions to conform existing types to new protocols.
- **Code Organization**: Separate functionality into extensions to keep code readable and maintainable.

## Summary

- Extensions add new functionality to existing types without subclassing.
- You can extend classes, structures, enumerations, and protocols.
- Extensions cannot add stored properties or override existing functionality. (remove it or find an example)
- Use extensions to conform types to protocols and organize code logically.

---

## References

- [Extensions](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html) - *The Swift Programming Language*
