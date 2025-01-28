# Properties (Stored and Computed)

In Swift, **properties** are variables and constants that are part of a class, structure, or enumeration. They associate values with a particular type. Properties can be divided into two main categories:

- **Stored Properties**: Store constant or variable values as part of an instance.
- **Computed Properties**: Calculate (rather than store) a value every time they are accessed.

Understanding these concepts is crucial for efficient Swift programming.

---

## Stored Properties

Stored properties are variables (`var`) or constants (`let`) that store values as part of an instance of a class or structure. They can have default values and can be modified during initialization.

### Example: Stored Properties in a Structure

```swift
struct FixedLengthRange {
    var firstValue: Int
    let length: Int
}

var range = FixedLengthRange(firstValue: 0, length: 3)
range.firstValue = 6
// range.length = 5 // Error: Cannot assign to property: 'length' is a 'let' constant
```

In this example:

- `firstValue` is a variable stored property that can be modified.
- `length` is a constant stored property that cannot be changed after initialization.

### Lazy Stored Properties

A **lazy stored property** is a property whose initial value is not calculated until the first time it is used. It's declared with the `lazy` keyword.

#### When to Use Lazy Properties

- When the initial value depends on outside factors that aren't known until after an instance is initialized.
- When the initial value is computationally expensive and should not be calculated unless needed.

#### Example: Lazy Stored Property

```swift
class DataImporter {
    var filename = "data.txt"
    // Data importing functionality
}

class DataManager {
    lazy var importer = DataImporter()
    var data = [String]()
    // Data management functionality
}

let manager = DataManager()
manager.data.append("Some data")
// The DataImporter instance is not created until 'importer' is accessed
print(manager.importer.filename) // Now 'importer' is initialized
```

**Key Points:**

- `importer` is not initialized until it's accessed.
- Useful for optimizing performance and resource usage.

---

## Computed Properties

Computed properties **do not store a value**. Instead, they provide a getter and an optional setter to retrieve and set other properties and values indirectly.

### Syntax of Computed Properties

```swift
var propertyName: Type {
    get {
        // Return some value of Type
    }
    set(newValue) {
        // Set a new value
    }
}
```

- **Getter**: Required. Returns a value.
- **Setter**: Optional. Allows you to modify related properties.

### Example: Computed Property in a Structure

```swift
struct Circle {
    var radius: Double
    
    var circumference: Double {
        get {
            return 2 * .pi * radius
        }
        set {
            radius = newValue / (2 * .pi)
        }
    }
}

var circle = Circle(radius: 5)
print(circle.circumference) // Outputs 31.41592653589793
circle.circumference = 62.83185307179586
print(circle.radius) // Outputs 10.0
```

**Explanation:**

- `circumference` computes the value based on `radius`.
- The setter updates the `radius` when `circumference` is set.

### Read-Only Computed Properties

If a computed property only has a getter, it's a **read-only** computed property.

#### Simplified Syntax for Read-Only Properties

```swift
var propertyName: Type {
    // Return some value of Type
}
```

#### Example: Read-Only Computed Property

```swift
struct Rectangle {
    var width: Double
    var height: Double
    
    var area: Double {
        return width * height
    }
}

let rect = Rectangle(width: 10, height: 5)
print(rect.area) // Outputs 50.0
// rect.area = 60.0 // Error: Cannot assign to property: 'area' is a get-only property
```

---

## Type Properties

Properties that are associated with the type itself rather than an instance of that type are called **type properties**. They are useful for defining values that are common to all instances.

### Stored Type Properties

Declared with the `static` keyword.

```swift
struct AudioChannel {
    static let thresholdLevel = 10
    static var maxInputLevelForAllChannels = 0
    var currentLevel: Int = 0 {
        didSet {
            if currentLevel > AudioChannel.thresholdLevel {
                // Cap the current level to the threshold level
                currentLevel = AudioChannel.thresholdLevel
            }
            if currentLevel > AudioChannel.maxInputLevelForAllChannels {
                // Store the new maximum input level
                AudioChannel.maxInputLevelForAllChannels = currentLevel
            }
        }
    }
}

var leftChannel = AudioChannel()
var rightChannel = AudioChannel()

leftChannel.currentLevel = 7
print(AudioChannel.maxInputLevelForAllChannels) // Outputs 7

rightChannel.currentLevel = 11
print(AudioChannel.maxInputLevelForAllChannels) // Outputs 10
```

**Explanation:**

- `thresholdLevel` is a constant type property.
- `maxInputLevelForAllChannels` is a variable type property shared among all instances.

### Computed Type Properties

Can be used with classes, structures, and enumerations.

```swift
class SomeClass {
    static var storedTypeProperty = "Some value."
    static var computedTypeProperty: Int {
        return 42
    }
    class var overrideableComputedTypeProperty: Int {
        return 27
    }
}
```

- `static` properties cannot be overridden in subclasses.
- `class` properties can be overridden.

---

## Key Concepts and Terminology

- **Property**: A value associated with a class, structure, or enumeration.
- **Stored Property**: Stores a constant or variable as part of an instance.
- **Computed Property**: Calculates a value every time it's accessed.
- **Lazy Property**: A property whose initial value is calculated only once when it's first accessed.
- **Property Observer**: Observes and responds to changes in a property's value.
- **Type Property**: A property that's associated with the type itself, not an instance.

---

## Conclusion
Properties in Swift provide flexibility and control over how values are stored and calculated in your types. By using stored and computed properties, lazy initialization, property observers, type properties, and property wrappers, you can write code that’s efficient, clear, and maintainable. 

With these tools, you can:

- Improve performance by using lazy properties to delay computations.
- Maintain data consistency with property observers.
- Share common data across all instances with type properties.
- Simplify property management using property wrappers.

---

**References:**

- [The Swift Programming Language - Properties](https://docs.swift.org/swift-book/LanguageGuide/Properties.html)
- [The Swift Programming Language - Access Control](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html)
- [The Swift Programming Language - Methods](https://docs.swift.org/swift-book/LanguageGuide/Methods.html)

---

## Questions
1. What are properties in Swift?
2. How are **stored properties** different from **computed properties**?
3. Can stored properties be constants (`let`) or variables (`var`)?
4. What is a **lazy stored property**?
5. When would you use a lazy property?
6. What keyword is used to declare a lazy property in Swift?
7. What is a **computed property**?
8. What are the main parts of a computed property?
9. When would you use a **read-only computed property**?
10. How can you simplify the syntax of a read-only computed property?
11. What are **type properties**, and when would you use them?
