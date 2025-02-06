Swift functions are powerful and versatile. They can be defined globally or nested within other functions. Additionally, understanding how closures escape or do not escape their defining scope is crucial for managing memory and ensuring your code runs as expected.


## Global Functions

Global functions are declared at the top level of your code and are accessible anywhere within the same module.

### Example

```swift
func sayHello() {
    print("Hello, World!")
}

sayHello() // Output: Hello, World!
```

### Characteristics

- **Scope**: Accessible throughout the module.
- **Use Cases**: Utility functions, mathematical computations, or any functionality that doesn't belong to a specific type.

---

## Nested Functions

Functions can be defined within other functions, creating a nested structure. Nested functions are not accessible outside their parent function.

### Example

```swift
func outerFunction() {
    func innerFunction() {
        print("This is the inner function.")
    }
    innerFunction()
}

outerFunction() // Output: This is the inner function.
```

### Capturing Values

Nested functions can capture and modify variables from their enclosing scope.

```swift
func makeCounter() -> () -> Int {
    var count = 0
    func increment() -> Int {
        count += 1
        return count
    }
    return increment
}

let counter = makeCounter()
print(counter()) // Output: 1
print(counter()) // Output: 2
```

### Benefits

- **Encapsulation**: Hide helper functions within other functions.
- **Organization**: Keep related functionality grouped together.

---

## Escaping and Non-Escaping Closures

Closures are self-contained blocks of functionality. Understanding how they escape or do not escape their defining scope is important for memory management and avoiding retain cycles.

### Non-Escaping Closures

By default, closures are non-escaping. They are executed within the function's scope and cannot be stored or called after the function returns.

#### Example

```swift
func performTask(task: () -> Void) {
    task()
    print("Task completed.")
}

performTask {
    print("Performing task...")
}

// Output:
// Performing task...
// Task completed.
```

### Escaping Closures

Escaping closures are marked with the `@escaping` keyword. They can be stored and called after the function in which they were passed has returned.
(Go a bit more in detail about `@escaping`)

#### Example

```swift
var completionHandlers: [() -> Void] = []

func addCompletionHandler(handler: @escaping () -> Void) {
    completionHandlers.append(handler)
}

addCompletionHandler {
    print("Completion handler called.")
}

// Later in the code
for handler in completionHandlers {
    handler()
}

// Output:
// Completion handler called.
```

### Use Cases for Escaping Closures

- **Asynchronous Operations**: Network requests, animations, or any tasks that complete after a delay.
- **Event Handling**: Storing closures to be called in response to events.

### Capturing `self` in Escaping Closures

When using `self` inside an escaping closure, you need to be cautious to prevent strong reference cycles.

#### Example with `[weak self]`

```swift
class MyClass {
    var value = 0

    func doSomething() {
        addCompletionHandler { [weak self] in
            guard let self = self else { return }
            print("Value is \(self.value)")
        }
    }
}
```

### Differences Between Escaping and Non-Escaping Closures

- **Performance**: Non-escaping closures can have optimizations applied by the compiler.
- **Memory Management**: Non-escaping closures do not require explicit capture lists for `self`.
- **Syntax**: Escaping closures may require you to use `self.` explicitly.

(change the wording to simple and keep it straightforward)

---

## Summary

- **Global Functions**: Useful for general-purpose functions accessible throughout your code.
- **Nested Functions**: Help organize code and encapsulate functionality.
- **Escaping Closures**: Allow closures to be stored and called later, but require careful memory management.
- **Non-Escaping Closures**: Default behavior, executed within the function's scope.

