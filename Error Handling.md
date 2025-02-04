# Error Handling in Swift

Error handling is a critical aspect of developing robust and reliable applications. Swift provides a rich set of features for throwing, catching, propagating, and manipulating recoverable errors at runtime.

## Introduction

Errors represent unexpected conditions that can occur during program execution. Swift's error handling model is designed to provide clear and expressive syntax for handling these situations gracefully.

## Representing and Throwing Errors

In Swift, errors are represented by values of types that conform to the `Error` protocol. This empty protocol indicates that a type can be used for error handling.

### Defining Custom Error Types

You can define your own error types using enumerations, structs, or classes that conform to the `Error` protocol.

```swift
enum FileError: Error {
    case fileNotFound
    case unreadable
    case encodingFailed
}
```

### Throwing Errors

Use the `throw` keyword to throw an error.

```swift
func readFile(at path: String) throws -> String {
    guard path == "validPath" else {
        throw FileError.fileNotFound
    }
    return "File content"
}
```

## Handling Errors

There are several ways to handle errors in Swift:

- **Propagating Errors**: Letting the calling function handle the error.
- **Handling with Do-Catch**: Using `do`-`catch` blocks.
- **Converting Errors to Optionals**: Using `try?`.
- **Disabling Error Propagation**: Using `try!`.

### Propagating Errors Using Throwing Functions

If a function can throw an error, it must be marked with the `throws` keyword. Errors thrown inside the function propagate to the calling scope.

```swift
func processFile() throws {
    let content = try readFile(at: "invalidPath")
    print(content)
}
```

### Handling Errors Using Do-Catch

Use `do`-`catch` blocks to handle errors.

```swift
do {
    let content = try readFile(at: "invalidPath")
    print(content)
} catch FileError.fileNotFound {
    print("The file was not found.")
} catch {
    print("An unexpected error occurred: \(error).")
}
```

### Converting Errors to Optional Values

Using `try?` converts the result to an optional. If an error is thrown, the result is `nil`.

```swift
let content = try? readFile(at: "invalidPath")
if let content = content {
    print(content)
} else {
    print("Failed to read the file.")
}
```

### Disabling Error Propagation

Using `try!` asserts that no error will be thrown. If an error does occur, the program will crash.

```swift
let content = try! readFile(at: "validPath")
print(content)
```

**Note**: Use `try!` only when you are certain that an error will not be thrown.

## Throwing Initializers

Initializers can throw errors, allowing you to handle initialization failures.

```swift
struct User {
    let name: String
    let age: Int

    init(name: String, age: Int) throws {
        guard age >= 0 else {
            throw InitializationError.invalidAge
        }
        self.name = name
        self.age = age
    }
}

enum InitializationError: Error {
    case invalidAge
}

do {
    let user = try User(name: "Alice", age: -1)
} catch InitializationError.invalidAge {
    print("Invalid age provided.")
}
```

## Rethrowing Functions and Closures

A function marked with `rethrows` can only throw an error if one of its function parameters throws an error.

```swift
func perform(operation: () throws -> Void) rethrows {
    try operation()
}

do {
    try perform {
        throw FileError.unreadable
    }
} catch {
    print("Operation failed with error: \(error).")
}
```

## Cleanup Actions with Defer

The `defer` statement defines a block of code that executes when the scope is exited, regardless of whether an error was thrown.

```swift
func openAndProcessFile() throws {
    print("Opening file.")
    defer {
        print("Closing file.")
    }
    throw FileError.unreadable
}

do {
    try openAndProcessFile()
} catch {
    print("Error occurred: \(error).")
}

// Output:
// Opening file.
// Closing file.
// Error occurred: unreadable.
```

## Error Handling in Asynchronous Code

When working with asynchronous operations, you often use completion handlers with a `Result` type.

```swift
func fetchData(completion: @escaping (Result<String, Error>) -> Void) {
    DispatchQueue.global().async {
        // Simulate a network request
        let success = false
        if success {
            completion(.success("Data received"))
        } else {
            completion(.failure(NetworkError.connectionLost))
        }
    }
}

enum NetworkError: Error {
    case connectionLost
}

fetchData { result in
    switch result {
    case .success(let data):
        print("Success: \(data)")
    case .failure(let error):
        print("Failure: \(error)")
    }
}
```

## Best Practices

- **Define Clear Error Types**: Use specific error types to provide more context.
- **Handle Errors Where Appropriate**: Catch errors where you can meaningfully handle them.
- **Avoid Overusing `try!`**: It can lead to runtime crashes if an error occurs.
- **Use `defer` for Cleanup**: Ensure resources are released properly.

## Summary

- Errors in Swift conform to the `Error` protocol.
- Use `throw` to throw an error.
- Handle errors using `do`-`catch` blocks.
- Propagate errors with functions marked `throws`.
- Use `try?` to convert errors to optionals, `try!` to assert no error will occur.
- Use `defer` to perform cleanup tasks.

---

## References

- [Error Handling](https://docs.swift.org/swift-book/LanguageGuide/ErrorHandling.html) - *The Swift Programming Language*
