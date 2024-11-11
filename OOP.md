# Object-Oriented Programming (OOP) 

Object-Oriented Programming (OOP) is a programming paradigm centered around objects rather than actions. It allows developers to create modular, reusable code by modeling real-world entities. Swift, as a modern programming language, supports OOP principles, enabling you to build robust and scalable applications.

This guide covers the core OOP concepts in Swift:

- Classes and Objects
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction

---

## 1. Classes and Objects

### Classes

A **class** is a blueprint for creating objects. It defines properties (attributes) and methods (functions) that describe the characteristics and behaviors of an object.
(make the definition a bit practical)

**Defining a Class:**

```swift
class Vehicle {
    var make: String
    var model: String
    var year: Int

    func startEngine() {
        print("Engine started.")
    }
}
```

### Objects (Instances)

An **object** is an instance of a class. It represents a concrete entity based on the class blueprint.
(change it to more pratical)

**Creating an Object:**

```swift
let car = Vehicle()
car.make = "Toyota"
car.model = "Corolla"
car.year = 2020
car.startEngine()  // Outputs: Engine started.
```

**Key Points:**

- Classes define the structure; objects are the actual instances.
- Objects have their own copy of properties but share the same methods.

---

## 2. Encapsulation
**Encapsulation** is the concept of bundling data (properties) and methods that operate on that data within a single unit (class) and restricting access to some of the object's components. This is a core principle in object-oriented programming that promotes modularity and code security.

### Access Control

Swift provides access control modifiers to enforce encapsulation. These modifiers determine where classes, properties, and methods can be accessed from:

- **`public`**: Accessible from any module.
- **`internal`**: Accessible within the same module (default).
- **`fileprivate`**: Accessible within the same file.
- **`private`**: Accessible within the enclosing declaration.

#### Example of Encapsulation

Below is an example of encapsulation in Swift, illustrating the use of the `private` access modifier to protect the `balance` property:

```swift
class BankAccount {
    private var balance: Double = 0.0

    func deposit(amount: Double) {
        balance += amount
    }

    func getBalance() -> Double {
        return balance
    }
}

let account = BankAccount()
account.deposit(amount: 1000)
// account.balance = 5000 // Error: 'balance' is private
print("Current balance: \(account.getBalance())")  // Outputs: Current balance: 1000.0
```

In this example, the `balance` property is marked as `private`, so it can't be accessed or modified directly outside of the `BankAccount` class. Instead, the class provides methods (`deposit` and `getBalance`) to interact with `balance` safely.

---


### Access Control Modifiers in Detail

1. **`public`**:
   - Allows classes, properties, and methods to be accessed from any module or file.
   - Typically used in libraries or frameworks to make specific elements available to other applications.
   - Example: A library might have a `public` class `NetworkManager` so it’s accessible by any app that imports the library.

   ```swift
   public class NetworkManager {
       public func fetchData() {
           // fetch data from an API
       }
   }
   ```

2. **`internal`** (Default):
   - The default access level in Swift.
   - Members marked as `internal` are accessible only within the same module. This is often used for code that needs to be shared across multiple files within an app but shouldn't be accessible outside of the app.
   - Example: The following `UserManager` class is accessible within the app module but not outside of it.

   ```swift
   internal class UserManager {
       internal func createUser() {
           // create a new user
       }
   }
   ```

3. **`fileprivate`**:
   - Limits the accessibility of properties and methods to the same file they’re declared in.
   - Useful for organizing code within a single file while hiding certain implementations from other parts of the app.
   - Example: The `TokenManager` class below has `fileprivate` properties and methods that can only be accessed within the same file.

   ```swift
   class TokenManager {
       fileprivate var token: String?

       fileprivate func generateToken() {
           token = "newToken123"
       }
   }
   ```

4. **`private`**:
   - Restricts access to properties and methods to the enclosing declaration (usually within the same class or struct).
   - Helps protect sensitive data by ensuring it can’t be accessed from outside the class.
   - Example: In the `BankAccount` class example above, the `balance` property is `private`, meaning it can only be accessed within the `BankAccount` class itself.

---


**Key Points:**

- Encapsulation protects the internal state of an object.
- Use methods to interact with the object's data safely.
- Access control modifiers restrict unauthorized access.

---

## 3. Inheritance

**Inheritance** allows a class to inherit properties and methods from another class. The class that inherits is called a **subclass**, and the class it inherits from is called a **superclass**.

### Example of Inheritance

```swift
class Animal {
    func eat() {
        print("Eating...")
    }
}

class Dog: Animal {
    func bark() {
        print("Woof!")
    }
}

let dog = Dog()
dog.eat()   // Inherited method
dog.bark()  // Subclass method
```


In Swift, we can create classes with methods (functions) that can be customized in subclasses. Two important concepts that help us do this are **method overriding** and **method overloading**.

### 1. Method Overriding

When a class is **subclassed** (a new class is created based on an existing one), the subclass can **override** methods from its **superclass** (the original class). This means the subclass can replace the method from the superclass with its own version, so it behaves differently. We use the `override` keyword in Swift to do this.

#### Why Override a Method?

Overriding is useful when you have a general method in the superclass but want a specific behavior in the subclass.

#### Example of Overriding

Imagine you have an `Animal` class with a method called `makeSound`. This method prints a general sound, "Some sound". But if we create a `Cat` subclass, we might want it to say "Meow" instead.

```swift
class Animal {
    func makeSound() {
        print("Some sound")
    }
}

class Cat: Animal {
    override func makeSound() {
        print("Meow")
    }
}

let cat = Cat()
cat.makeSound()  // Outputs: Meow
```

- Here, the `Cat` class overrides the `makeSound` method from `Animal`.
- When `cat.makeSound()` is called, it prints "Meow" instead of "Some sound".

Without the `override` keyword, Swift will throw an error, as it expects you to use `override` when replacing methods in subclasses. This ensures you're aware of the changes to inherited behavior.

#### Another Example

Let’s imagine we have a superclass `Vehicle` with a method `startEngine`. We want our `Car` subclass to have a different engine start sound.

```swift
class Vehicle {
    func startEngine() {
        print("Engine starting...")
    }
}

class Car: Vehicle {
    override func startEngine() {
        print("Car engine roaring to life!")
    }
}

let myCar = Car()
myCar.startEngine()  // Outputs: Car engine roaring to life!
```

Here, `Car` overrides `startEngine` so that it prints a specific message, while `Vehicle` has a more general message.

---

### 2. Method Overloading

**Method overloading** is different from overriding. Instead of replacing an existing method, overloading lets us create multiple methods with the **same name** in the same class, as long as they have different **parameters** (inputs). This way, you can use the same method name to handle different types or numbers of inputs.

#### Why Overload a Method?

Overloading makes code easier to read and use. You can use the same name for similar actions, which lets you keep method names simple and consistent.

#### Example of Overloading

Suppose we want to create a class called `Calculator` that can add two numbers together. However, we might want to use the `add` method to add either two integers or two doubles. With overloading, we can create two `add` methods with different types of inputs.

```swift
class Calculator {
    func add(a: Int, b: Int) -> Int {
        return a + b
    }

    func add(a: Double, b: Double) -> Double {
        return a + b
    }
}

let calculator = Calculator()
print(calculator.add(a: 5, b: 10))       // Outputs: 15
print(calculator.add(a: 5.5, b: 10.2))   // Outputs: 15.7
```

In this example:
- We have two `add` methods in the `Calculator` class.
- One `add` method takes integers, and the other takes doubles.
- Swift automatically knows which `add` method to call based on the types of `a` and `b`.

#### Another Example: Overloading with Different Number of Parameters

You can also overload a method by changing the number of parameters. Here’s an example using the same `Calculator` class:

```swift
class Calculator {
    func multiply(a: Int, b: Int) -> Int {
        return a * b
    }

    func multiply(a: Int, b: Int, c: Int) -> Int {
        return a * b * c
    }
}

let calculator = Calculator()
print(calculator.multiply(a: 2, b: 3))          // Outputs: 6
print(calculator.multiply(a: 2, b: 3, c: 4))    // Outputs: 24
```

In this example:
- The `multiply` method is overloaded to take either two or three integers.
- Swift will use the correct method depending on whether two or three numbers are given.

---
**Key Points:**

- Inheritance promotes code reusability.
- Use `override` to modify inherited methods.
- Swift classes do not inherit from a universal base class. (remove it for now)

---

## 4. Polymorphism

**Polymorphism** allows objects to be treated as instances of their superclass rather than their actual class. It enables one interface to be used for a general class of actions.

### Example of Polymorphism

```swift
class Employee {
    func work() {
        print("Working...")
    }
}

class Developer: Employee {
    override func work() {
        print("Writing code.")
    }
}

class Designer: Employee {
    override func work() {
        print("Designing interfaces.")
    }
}

let employees: [Employee] = [Developer(), Designer()]

for employee in employees {
    employee.work()
}
// Outputs:
// Writing code.
// Designing interfaces.
```

**Key Points:**

- Polymorphism lets us use a superclass reference to call a method, which then runs the specific version of that method defined in the subclass.
- It enhances flexibility and integration.

---

## 5. Abstraction

**Abstraction** involves hiding complex implementation details and showing only the necessary features of an object.

### Using Protocols for Abstraction

In Swift, **protocols** can be used to define abstract interfaces that classes or structures can adopt.

```swift
protocol Shape {
    var area: Double { get }
}

class Circle: Shape {
    var radius: Double

    var area: Double {
        return .pi * radius * radius
    }

    init(radius: Double) {
        self.radius = radius
    }
}

class Rectangle: Shape {
    var width: Double
    var height: Double

    var area: Double {
        return width * height
    }

    init(width: Double, height: Double) {
        self.width = width
        self.height = height
    }
}

let shapes: [Shape] = [Circle(radius: 5), Rectangle(width: 10, height: 20)]

for shape in shapes {
    print("Area: \(shape.area)")
}
// Outputs:
// Area: 78.53981633974483
// Area: 200.0
```

**Key Points:**

- Abstraction simplifies code by exposing only necessary details.
- Protocols define methods and properties that conforming types must implement.
- Classes and structures can adopt protocols.

---

## Summary

- **Classes and Objects**: Classes are blueprints; objects are instances.
- **Encapsulation**: Bundles data and methods, restricts access.
- **Inheritance**: Subclasses inherit from superclasses, promoting code reuse.
- **Polymorphism**: Allows methods to be used generically across different classes.
- **Abstraction**: Hides implementation details, exposing only necessary features.

Understanding these OOP concepts in Swift helps you write clean, maintainable, and scalable code. By applying these principles, you can model real-world entities effectively and enhance the quality of your applications.

---

## References

- [The Swift Programming Language - Classes and Structures](https://docs.swift.org/swift-book/LanguageGuide/ClassesAndStructures.html)
- [The Swift Programming Language - Inheritance](https://docs.swift.org/swift-book/LanguageGuide/Inheritance.html)
- [The Swift Programming Language - Methods](https://docs.swift.org/swift-book/LanguageGuide/Methods.html)
- [The Swift Programming Language - Protocols](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)

---

## Questions
1. What is Object-Oriented Programming (OOP) focused on?
2. How does Swift support the core OOP concepts?
3. What is a class in Swift, and what does it contain?
4. How would you create an object from a class in Swift?
5. What is encapsulation, and why is it useful?
6. Which access control modifier would you use to restrict access to a class property within the same class only?
7. Why might you use a `private` property in a class?
8. How does inheritance promote code reuse?
9. What keyword do you use to override a method in a subclass?
10. Why would you override a superclass method in a subclass?
11. How is method overloading different from method overriding?
12. Can you give an example of method overloading with different parameter types?
13. What is polymorphism, and how does it work in Swift?
14. How does polymorphism increase flexibility in your code?
15. What is abstraction, and why is it beneficial in OOP?
16. How are protocols used to achieve abstraction in Swift?
17. What would happen if two different classes adopted the same protocol in Swift?
18. How does encapsulation contribute to code security?
19. Why might you use polymorphism when working with arrays of different object types?
20. What are the main benefits of using OOP principles in Swift programming?