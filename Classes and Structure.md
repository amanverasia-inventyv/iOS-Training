# Classes, Structures, and the `self` Keyword

In Swift, **classes** and **structures** are foundational building blocks for your code. They allow you to create custom data types with properties and methods. Understanding the differences between them and how to use the `self` keyword is essential for effective Swift programming.

---

## Classes

A **class** is like a template or blueprint that defines how to create objects with specific properties and behaviors. When you create an object from a class, it becomes an instance of that class. Classes also allow you to share common features with other classes through a concept called inheritance. Additionally, classes are reference types, which means that multiple variables can refer to the same object in memory.

### Defining a Class

```swift
class Person {
    var name: String
    var age: Int
    
    func greet() {
        print("Hello, my name is \(name).")
    }
}
```

- **Properties**: Variables inside the class (`name`, `age`).
- **Methods**: Functions inside the class (`greet()`).

### Creating an Instance

```swift
let person = Person()
person.name = "Alice"
person.age = 30
person.greet()  // Outputs: Hello, my name is Alice.
```

### Reference Types

Classes are **reference types**, meaning that when you assign or pass them around, you're working with references to the same instance.

```swift
let personA = Person()
personA.name = "Bob"

let personB = personA
personB.name = "Charlie"

print(personA.name)  // Outputs: Charlie
```

- Both `personA` and `personB` point to the same `Person` instance.

---

## Structures

A **structure** is similar to a class but is a **value type**.

### Defining a Structure

```swift
struct Point {
    var x: Double
    var y: Double
    
    func description() {
        print("Point at (\(x), \(y))")
    }
}
```

### Creating an Instance

```swift
var point1 = Point(x: 1.0, y: 2.0)
var point2 = point1  // Creates a copy

point2.x = 3.0

point1.description()  // Outputs: Point at (1.0, 2.0)
point2.description()  // Outputs: Point at (3.0, 2.0)
```

### Value Types

Structures are **value types**, meaning they make a copy of themselves when assigned to a new variable or constant.


---

## Differences Between Classes and Structures

- **Inheritance**:
  - **Classes** can inherit from other classes.
  - **Structures** cannot inherit from other structures.

- **Type**:
  - **Classes** are reference types.
  - **Structures** are value types.

- **Identity Operators**:
  - Use = = = and ! = = to check if two class references point to the same instance.

- **Deinitializers**:
  - **Classes** can have deinitializers (`deinit`).
  - **Structures** cannot have deinitializers.

- **Initializers**:
  - **Classes** can have multiple custom initializers, but they do not have a default initializer unless provided.
  - **Structures** have a default initializer if no custom initializer is defined, and you can add custom initializers as needed.

---

## The `self` Keyword

The `self` keyword refers to the current instance of a class or structure. It is used to:

- Access properties and methods within the instance.
- Differentiate between property names and parameter names in methods and initializers.

### Using `self` in Methods

```swift
class Circle {
    var radius: Double
    
    init(radius: Double) {
        self.radius = radius  // 'self.radius' refers to the property
    }
    
    func area() -> Double {
        return self.radius * self.radius * .pi
    }
}
```

- In the initializer, `self.radius` distinguishes the property from the parameter `radius`.

### To Note

- You can omit `self` when there's no ambiguity.
- It's required when a parameter name matches a property name.

---

## When to Use Classes vs. Structures

**Use a Structure When:**

- You need to model simple data types.
- You want copies to have independent states.
- The data will be used in code across multiple threads.

**Use a Class When:**

- You need inheritance to define hierarchical relationships.
- You want to control the identity of the data (reference semantics).
- The data will be shared or mutated across different parts of your code.

---

## Simple Examples
### Class Example

```swift
class Vehicle {
    var currentSpeed = 0.0

    func accelerate(by amount: Double) {
        currentSpeed += amount
    }
}

let car = Vehicle()
car.accelerate(by: 20.0)
print(car.currentSpeed)  // Outputs: 20.0
```

### Structure Example

```swift
struct Vehicle {
    var currentSpeed = 0.0

    mutating func accelerate(by amount: Double) {
        currentSpeed += amount
    }
}

let vehicle1 = Vehicle(currentSpeed: 10.0)
var vehicle2 = vehicle1  // Creates a copy
vehicle2.accelerate(by: 20.0)

print(vehicle1.currentSpeed)  // Outputs: 10.0
print(vehicle2.currentSpeed)  // Outputs: 30.0
```

In this example, `vehicle2` is a copy of `vehicle1`, so changes to `vehicle2` do not affect `vehicle1`.

---

## Conclusion

- **Classes** are reference types that support inheritance and are suitable for complex data models.
- **Structures** are value types ideal for simple data containers.
- Use the `self` keyword to access instance properties and methods, especially when names conflict.

Understanding these concepts helps you decide how to structure your code and manage data effectively in Swift.

---

## Questions
1. What is the main difference between a class and a structure in Swift?
2. How would you define a property inside a class?
3. What is a **reference type** in Swift?
4. Why does changing a property in one instance of a class affect another variable pointing to the same instance?
5. What does it mean that structures are **value types**?
6. If you assign a structure to a new variable, what happens to the original structure's values?
7. How does inheritance work in classes? Can structures inherit properties or methods?
8. When would you choose to use a structure instead of a class?
9. What is the `self` keyword used for in Swift?
10. Why would you use `self` inside an initializer or method?
11. Can you omit `self` in a method? When would you need to include it?
12. How do you check if two variables point to the same instance of a class?
13. What keyword is used to release resources when a class instance is no longer needed?
14. Can structures have deinitializers? Why or why not?
15. How does Swift provide a default initializer for structures?
16. Why might you need to create custom initializers in both classes and structures?
17. What are some scenarios where a class would be more appropriate than a structure?
18. How do you create an instance of a class in Swift?
19. How do you create an instance of a structure in Swift?
20. In the example where `vehicle1` and `vehicle2` are instances of a structure, why does changing `vehicle2` not affect `vehicle1`?
