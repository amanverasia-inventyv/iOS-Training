# Initialization & Deinitialization

Initialization and deinitialization are fundamental concepts in Swift programming that ensure your custom types are correctly set up and cleaned up. This guide delves into these topics, explaining how to initialize and deinitialize classes, structures, and enumerations in Swift.

---

## Initialization

**Initialization** is the process of preparing an instance of a class, structure, or enumeration for use. It involves setting an initial value for each stored property and performing any necessary setup.

### Initializers

Initializers are special methods that provide initial values for properties and perform setup. They are defined using the `init` keyword.

### Default Initializers

Swift provides a default initializer for any structure or class that provides default values for all of its properties and doesn't define any custom initializers.

```swift
struct Fahrenheit {
    var temperature = 32.0
}

let defaultFahrenheit = Fahrenheit()
print("The default temperature is \(defaultFahrenheit.temperature)° Fahrenheit.")
// Outputs: The default temperature is 32.0° Fahrenheit.
```

### Custom Initializers

You can define custom initializers to set up your type according to specific needs.

#### Example: Custom Initializer with Parameters

```swift
struct Celsius {
    var temperatureInCelsius: Double

    init(fromFahrenheit fahrenheit: Double) {
        temperatureInCelsius = (fahrenheit - 32.0) / 1.8
    }

    init(fromKelvin kelvin: Double) {
        temperatureInCelsius = kelvin - 273.15
    }
}

let bodyTemperature = Celsius(fromFahrenheit: 98.6)
print("Body temperature in Celsius: \(bodyTemperature.temperatureInCelsius)")
// Outputs: Body temperature in Celsius: 37.0
```

**Explanation:**

- The `Celsius` struct has two custom initializers.
- Each initializer sets `temperatureInCelsius` based on different input parameters.

### Memberwise Initializers for Structures

Structures automatically receive a memberwise initializer if they do not define any custom initializers.

```swift
struct Size {
    var width: Double
    var height: Double
}

let size = Size(width: 10.0, height: 20.0)
```

### Initializer Parameters and Argument Labels

You can provide external parameter names and argument labels to make your initializers more expressive.

```swift
struct Color {
    var red, green, blue: Double

    init(red: Double, green: Double, blue: Double) {
        self.red = red
        self.green = green
        self.blue = blue
    }
}

let magenta = Color(red: 1.0, green: 0.0, blue: 1.0)
```

### The `self` Property in Initializers

Within an initializer, `self` refers to the instance being initialized. Use `self` to distinguish between property names and parameter names if they are the same.

```swift
struct Point {
    var x: Double
    var y: Double

    init(x: Double, y: Double) {
        self.x = x
        self.y = y
    }
}
```

### Initializer Delegation for Value Types

You can define multiple initializers and have them call each other to reuse code, a process known as **initializer delegation**.

```swift
struct Rectangle {
    var width: Double
    var height: Double

    // Custom initializer
    init(width: Double, height: Double) {
        self.width = width
        self.height = height
    }

    // Delegating initializer
    init(squareWithSide side: Double) {
        self.init(width: side, height: side)
    }
}

let square = Rectangle(squareWithSide: 5.0)
print("Square width: \(square.width), height: \(square.height)")
// Outputs: Square width: 5.0, height: 5.0
```

### Classes and Inheritance

Class initializers are more complex due to inheritance. Swift ensures that all stored properties are initialized before an instance is used.

#### Designated and Convenience Initializers

- **Designated Initializers**: Primary initializers that fully initialize all properties introduced by that class and call an appropriate superclass initializer.
- **Convenience Initializers**: Secondary initializers that must call a designated initializer from the same class.

#### Initialization Rules for Class Types

1. A designated initializer must call a designated initializer from its immediate superclass.
2. A convenience initializer must call another initializer from the same class.
3. A convenience initializer must ultimately call a designated initializer.

#### Example: Class Initialization

```swift
class Vehicle {
    var numberOfWheels: Int

    init() {
        numberOfWheels = 0
    }
}

class Bicycle: Vehicle {
    override init() {
        super.init()
        numberOfWheels = 2
    }
}

let bike = Bicycle()
print("Bike has \(bike.numberOfWheels) wheels.")
// Outputs: Bike has 2 wheels.
```

**Explanation:**

- `Vehicle` has a designated initializer.
- `Bicycle` overrides the initializer, calls `super.init()`, and modifies `numberOfWheels`.

### Failable Initializers

Sometimes, initialization can fail. Swift allows you to define **failable initializers** that can return `nil`.

```swift
struct Animal {
    let species: String

    init?(species: String) {
        if species.isEmpty {
            return nil
        }
        self.species = species
    }
}

if let someCreature = Animal(species: "") {
    print("An animal was initialized with a species of \(someCreature.species)")
} else {
    print("The species was empty, so initialization failed.")
}
// Outputs: The species was empty, so initialization failed.
```

### Required Initializers

Use the `required` keyword to indicate that every subclass must implement that initializer.

```swift
class SomeClass {
    required init() {
        // initializer implementation
    }
}

class SomeSubclass: SomeClass {
    required init() {
        // subclass implementation
    }
}
```

---

## Deinitialization

**Deinitialization** is the process of preparing an instance of a class for deallocation. Swift automatically deallocates instances when they are no longer needed, but you can perform additional cleanup using a deinitializer.

### Deinitializer Syntax

Deinitializers are defined using the `deinit` keyword and do not take any parameters.

```swift
class BankAccount {
    var balance: Double

    init(balance: Double) {
        self.balance = balance
        print("Account created with balance: \(balance)")
    }

    deinit {
        print("Account with balance \(balance) is being deinitialized.")
    }
}

var account: BankAccount? = BankAccount(balance: 1000.0)
account = nil
// Outputs:
// Account created with balance: 1000.0
// Account with balance 1000.0 is being deinitialized.
```

**Key Points:**

- Deinitializers are called automatically just before instance deallocation.
- They are only available for classes (reference types), not structures or enumerations (value types).
- Each class can have only one deinitializer.

### Use Cases for Deinitializers

- Closing file descriptors.
- Removing observers.
- Releasing resources like network connections.
- Performing any necessary cleanup.

---

## Lazy Properties and Initialization

A **lazy stored property** is a property whose initial value is not calculated until the first time it is used. This is particularly useful when the initial value is dependent on external factors or when it is computationally expensive to create.

### Example: Lazy Property with Initialization

```swift
class DataImporter {
    var filename = "data.txt"
    init() {
        print("DataImporter initialized.")
    }
    // Data importing functionality
}

class DataManager {
    lazy var importer = DataImporter()
    var data = [String]()
    // Data management functionality
}

let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
// At this point, DataImporter has not been initialized

print(manager.importer.filename)
// Outputs:
// DataImporter initialized.
// data.txt
```

**Explanation:**

- The `importer` property is marked as `lazy`, so `DataImporter` is not initialized until `importer` is accessed.
- When `manager.data.append` is called, `importer` is still `nil`.
- Accessing `manager.importer.filename` triggers the initialization of `DataImporter`.

**When to Use Lazy Properties:**

- When the property's initial value is dependent on external factors not known until after an instance is initialized.
- When the property's initial value is computationally expensive to create and you want to delay this cost until it's needed.

---

## Initializer Delegation for Class Types

Class initializers can delegate across the class hierarchy, ensuring all properties are properly initialized.

### Two-Phase Initialization

Swift uses a two-phase initialization process:

1. **Phase 1**: Each stored property is assigned an initial value.
2. **Phase 2**: Each class is given the opportunity to customize its stored properties further.

### Safety Checks

Swift enforces safety checks to ensure that all properties are initialized before use:

- A designated initializer must ensure that all properties introduced by its class are initialized before it delegates up to a superclass initializer.
- A designated initializer must call its superclass initializer before assigning a value to an inherited property.
- Until Phase 1 is complete, the instance is not fully initialized, and you cannot access properties or call methods.

---

## Key Concepts and Terminology

- **Initialization**: The process of setting up an instance of a class, structure, or enumeration by assigning initial values to stored properties.
- **Initializer**: A special method defined with `init` that sets initial values and performs setup.
- **Default Initializer**: An automatic initializer Swift provides if no custom initializers are defined and all properties have default values.
- **Custom Initializer**: An initializer that allows specific setup, often with parameters for custom configuration.
- **Memberwise Initializer**: A default initializer for structures that assigns values to each property.
- **Failable Initializer**: An initializer that can return `nil` if initialization fails, defined with `init?`.
- **Designated Initializer**: The primary initializer that fully initializes a class's properties and calls a superclass initializer.
- **Convenience Initializer**: A secondary initializer that calls a designated initializer within the same class.
- **Required Initializer**: An initializer that must be implemented by every subclass, marked with `required`.
- **Initializer Delegation**: A process where one initializer calls another to avoid code duplication.
- **Deinitialization**: The process of cleaning up an instance before it's deallocated, defined with `deinit`.
- **Two-Phase Initialization**: Swift's safety mechanism ensuring properties are initialized before customization.
- **Lazy Initialization**: Delays initialization of a property until it's first accessed to save resources.

---

## Conclusion

Initialization and deinitialization are crucial for managing the lifecycle of instances in Swift. By understanding how to properly initialize your types and clean up resources when they're no longer needed, you can write robust and efficient code.

Key takeaways:

- **Proper Initialization**: Ensure all properties are initialized before use.
- **Lazy Initialization**: Optimize performance by delaying property creation until necessary.
- **Resource Management**: Use deinitializers to release resources and prevent memory leaks.
- **Initializer Delegation**: Reuse initialization code through delegation.

By mastering these concepts, you'll be better equipped to handle complex initialization scenarios and write cleaner, more maintainable Swift code.

---

**References:**

- [The Swift Programming Language - Initialization](https://docs.swift.org/swift-book/LanguageGuide/Initialization.html)
- [The Swift Programming Language - Deinitialization](https://docs.swift.org/swift-book/LanguageGuide/Deinitialization.html)
- [The Swift Programming Language - Automatic Reference Counting](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html)

---

## Questions
1. What is an initializer in Swift?
2. How is a default initializer different from a custom initializer?
3. What is the purpose of a memberwise initializer in a structure?
4. How do you create a custom initializer with parameters?
5. When would you use a failable initializer?
6. What is a designated initializer?
7. What’s the role of a convenience initializer?
8. What does a required initializer enforce?
9. How does initializer delegation help in Swift?
10. What is deinitialization, and when is it used?
11. Can structures have deinitializers?
12. Explain Swift’s two-phase initialization process.
13. Why would you use lazy initialization for a property?
14. How does a lazy stored property differ from a regular stored property?
15. How do class initializers handle inheritance?