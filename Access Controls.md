# Access Control in Swift

Swift provides a robust access control system that lets you specify the visibility and accessibility of your classes, properties, methods, and other entities. Proper use of access control helps encapsulate your code and protect implementation details.

## Access Levels

Swift has five access levels:

1. **Open**
2. **Public**
3. **Internal**
4. **Fileprivate**
5. **Private**

These levels determine where your entities can be accessed within your code.

### 1. Open

- **Usage**: Only for classes and class members.
- **Accessibility**: Available outside the module and can be subclassed or overridden.
- **Characteristics**:
  - The highest (least restrictive) access level.
  - Allows other modules to inherit and override.

#### Example

```swift
// In Module A
open class OpenClass {
    open func greet() {
        print("Hello from OpenClass!")
    }
}

// In Module B
import ModuleA

class SubClass: OpenClass {
    override func greet() {
        print("Hello from SubClass!")
    }
}

let instance = SubClass()
instance.greet() // Output: Hello from SubClass!
```

### 2. Public

- **Usage**: Classes, functions, properties, etc.
- **Accessibility**: Available outside the module but cannot be subclassed or overridden outside the module.
- **Characteristics**:
  - Entities are accessible but not extensible.

#### Example

```swift
// In Module A
public class PublicClass {
    public func greet() {
        print("Hello from PublicClass!")
    }
}

// In Module B
import ModuleA

let instance = PublicClass()
instance.greet() // Output: Hello from PublicClass!

// Error: Cannot subclass 'PublicClass' outside of its defining module
// class SubClass: PublicClass { }
```

### 3. Internal

- **Usage**: Default access level if none is specified.
- **Accessibility**: Accessible within the same module.
- **Characteristics**:
  - Suitable for most entities within an app or framework.
  - Not accessible outside the module.

#### Example

```swift
class InternalClass {
    func greet() {
        print("Hello from InternalClass!")
    }
}

let instance = InternalClass()
instance.greet() // Output: Hello from InternalClass!

// In another module, InternalClass is not accessible.
```

### 4. Fileprivate

- **Usage**: Limits access to the current Swift file.
- **Accessibility**: Accessible within the file it's declared.
- **Characteristics**:
  - Useful for hiding implementation details within a file.
  - Allows sharing among multiple classes or extensions in the same file.

#### Example

```swift
fileprivate class FilePrivateClass {
    fileprivate func greet() {
        print("Hello from FilePrivateClass!")
    }
}

class AnotherClassInSameFile {
    func test() {
        let instance = FilePrivateClass()
        instance.greet() // Accessible here
    }
}

// In a different file, FilePrivateClass is not accessible.
```

### 5. Private

- **Usage**: Restricts access to the enclosing declaration.
- **Accessibility**: Accessible only within the enclosing class or struct.
- **Characteristics**:
  - The most restrictive access level.
  - Does not allow access from extensions or subclasses.

#### Example

```swift
class PrivateClass {
    private var secret = "Hidden Message"
    
    func revealSecret() {
        print(secret)
    }
}

extension PrivateClass {
    func tryAccessSecret() {
        // print(secret) // Error: 'secret' is inaccessible due to 'private' protection level
    }
}
```

## Access Control for Properties and Classes

Access control can be applied to individual properties and methods within a class or struct.

### Public Properties and Methods

```swift
public class Car {
    public var model: String
    public var year: Int
    
    public init(model: String, year: Int) {
        self.model = model
        self.year = year
    }
    
    public func displayInfo() {
        print("Car: \(model), Year: \(year)")
    }
}

// Accessible from any module
let car = Car(model: "Tesla", year: 2023)
car.displayInfo() // Output: Car: Tesla, Year: 2023
```

### Private Properties

```swift
class Account {
    private var balance: Double = 0.0
    
    func deposit(amount: Double) {
        balance += amount
    }
    
    func getBalance() -> Double {
        return balance
    }
}

let account = Account()
account.deposit(amount: 100.0)
print(account.getBalance()) // Output: 100.0
// account.balance // Error: 'balance' is inaccessible due to 'private' protection level
```

## Access Control and Inheritance

- **Open Classes**: Can be subclassed and overridden both within and outside the module.
- **Public Classes**: Can be subclassed and overridden within the same module only.
- **Internal, Fileprivate, Private Classes**: Subclassing and overriding depend on their access level and location.

#### Example with Open Class

```swift
// In Module A
open class Shape {
    open func draw() {
        print("Drawing a shape.")
    }
}

// In Module B
import ModuleA

class Circle: Shape {
    override func draw() {
        print("Drawing a circle.")
    }
}

let circle = Circle()
circle.draw() // Output: Drawing a circle.
```

#### Example with Public Class

```swift
// In Module A
public class Vehicle {
    public func startEngine() {
        print("Engine started.")
    }
}

// In Module A (same module)
class Car: Vehicle {
    override func startEngine() {
        print("Car engine started.")
    }
}

// In Module B
import ModuleA

// Error: Cannot subclass 'Vehicle' outside of its defining module
// class Bike: Vehicle { }
```

## Fileprivate vs. Private

- **Private**: Restricts access to the enclosing declaration.
- **Fileprivate**: Restricts access to the entire file.

#### Private Example

```swift
class Container {
    private var items: [String] = []
    
    private func addItem(_ item: String) {
        items.append(item)
    }
    
    func performAction() {
        addItem("New Item")
    }
}

extension Container {
    func tryAddingItem() {
        // addItem("Another Item") // Error: 'addItem' is inaccessible due to 'private' protection level
    }
}
```

#### Fileprivate Example

```swift
fileprivate class Helper {
    fileprivate func assist() {
        print("Assisting...")
    }
}

class Manager {
    func delegate() {
        let helper = Helper()
        helper.assist() // Accessible here
    }
}

// In the same file, Helper and its methods are accessible.
```

## Best Practices

- **Default to Internal**: Use the default internal access level unless you need to expose entities outside the module.
- **Use Private for Encapsulation**: Hide internal implementation details that should not be accessed directly.
- **Leverage Fileprivate for Shared Implementation**: Use fileprivate when multiple entities in the same file need access.
- **Choose Open Carefully**: Use open only when you want to allow subclassing and overriding outside the module.

## Summary

- **Open**: Most permissive; allows subclassing and overriding outside the module.
- **Public**: Accessible outside the module; no subclassing or overriding outside the module.
- **Internal**: Accessible within the module; default access level.
- **Fileprivate**: Accessible within the same file.
- **Private**: Accessible within the enclosing declaration.

Understanding and properly applying access control levels ensures your code's integrity and maintains proper encapsulation.

---

## References

- [Access Control](https://docs.swift.org/swift-book/LanguageGuide/AccessControl.html) - *The Swift Programming Language*
