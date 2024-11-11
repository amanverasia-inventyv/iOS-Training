# Type Casting

This note explores **type casting** in Swift—a powerful feature that allows you to check and interpret the type of an instance at runtime. We'll cover checking types, upcasting, downcasting, and how to work with the `Any` and `AnyObject` types. Along the way, we'll explain new concepts as they arise, providing code examples for clarity.

---

## Introduction

In Swift, type casting is used to:

- **Check the type** of an instance.
- **Treat an instance as a different superclass or subclass** from somewhere else in its class hierarchy.

Type casting in Swift is implemented with the `is` and `as` operators:

- `is`: Checks if an instance is of a certain subclass type.
- `as`: Casts an instance to a different type.

Understanding type casting is essential for working with complex data structures, especially when dealing with collections that can hold instances of multiple types.

---

## Type Hierarchy in Swift

Before diving into type casting, it's important to understand the concept of class hierarchies in Swift.

### Classes and Inheritance

Classes can inherit from other classes, forming a hierarchy. A subclass inherits properties and methods from its superclass.

```swift
class Vehicle {
    var currentSpeed: Double = 0.0

    func description() -> String {
        return "Traveling at \(currentSpeed) km/h"
    }
}

class Car: Vehicle {
    var gear: Int = 1

    override func description() -> String {
        return super.description() + " in gear \(gear)"
    }
}

class Bicycle: Vehicle {
    var hasBasket: Bool = false
}

class Train: Vehicle {
    var numberOfCarriages: Int = 0

    override func description() -> String {
        return super.description() + " with \(numberOfCarriages) carriages"
    }
}
```

In this example:

- `Vehicle` is the superclass.
- `Car`, `Bicycle`, and `Train` are subclasses of `Vehicle`.
- Each subclass adds its own properties and methods.

---

## Checking Type with `is`

The `is` operator checks if an instance is of a certain subclass type. It returns `true` if the instance is of that type or a subclass of that type, and `false` otherwise.

### Example: Type Checking with `is`

```swift
let someVehicle: Vehicle = Car()

if someVehicle is Car {
    print("someVehicle is a Car")
} else {
    print("someVehicle is not a Car")
}
// Outputs: someVehicle is a Car
```

**Explanation:**

- `someVehicle` is declared as `Vehicle` but is actually an instance of `Car`.
- The `is` operator checks if `someVehicle` is of type `Car` or its subclasses.

---

## Downcasting

Downcasting is the process of treating an instance as if it were a subclass of its current type. Swift provides two operators for downcasting:

- **Conditional downcast (`as?`)**: Returns an optional value; it will be `nil` if the downcast fails.
- **Forced downcast (`as!`)**: Forces the downcast and triggers a runtime error if it fails.

### Optional Downcasting with `as?`

Use `as?` when you're not sure if the downcast will succeed.

```swift
let someVehicle: Vehicle = Car()

if let car = someVehicle as? Car {
    print("This vehicle is a car with gear \(car.gear)")
} else {
    print("This vehicle is not a car")
}
// Outputs: This vehicle is a car with gear 1
```

**Explanation:**

- Attempts to downcast `someVehicle` to `Car`.
- If successful, `car` is an optional `Car` instance.

### Forced Downcasting with `as!`

Use `as!` when you're certain the downcast will succeed. Be cautious, as a failed forced downcast will cause a runtime error.

```swift
let someVehicle: Vehicle = Car()

let car = someVehicle as! Car
print("This vehicle is a car with gear \(car.gear)")
// Outputs: This vehicle is a car with gear 1
```

**Runtime Error Example:**

```swift
let anotherVehicle: Vehicle = Bicycle()

let car = anotherVehicle as! Car
// Runtime Error: Could not cast value of type 'Bicycle' to 'Car'
```

---

## Upcasting

Upcasting is the process of treating an instance as its superclass type. In Swift, upcasting is implicit and doesn't require any special syntax.

### Example: Upcasting

```swift
let car = Car()
let vehicle: Vehicle = car // Implicit upcasting

print(vehicle.description())
// Outputs: Traveling at 0.0 km/h in gear 1
```

**Explanation:**

- `car` is an instance of `Car`.
- Assigning `car` to `vehicle` implicitly upcasts it to `Vehicle`.
- Methods and properties accessible via `Vehicle` are still available.

---

## Type Casting for `Any` and `AnyObject`

Swift provides two special types:

- **`Any`**: Can represent an instance of any type, including function types.
- **`AnyObject`**: Can represent an instance of any class type.

### Using `Any`

`Any` can hold any type, including value types like `Int`, `Double`, `Bool`, and even functions.

```swift
var items: [Any] = []

items.append(42)
items.append(3.14)
items.append("Hello, Swift!")
items.append((3.0, 5.0))
items.append({ (name: String) -> String in "Hello, \(name)" })
```

### Casting from `Any` to a Specific Type

When retrieving items from an `Any` array, you need to downcast to the expected type.

```swift
for item in items {
    switch item {
    case let number as Int:
        print("Integer: \(number)")
    case let number as Double:
        print("Double: \(number)")
    case let text as String:
        print("String: \(text)")
    case let tuple as (Double, Double):
        print("Tuple: \(tuple)")
    case let closure as (String) -> String:
        print(closure("World"))
    default:
        print("Unknown type")
    }
}
// Outputs:
// Integer: 42
// Double: 3.14
// String: Hello, Swift!
// Tuple: (3.0, 5.0)
// Hello, World
```

### Using `AnyObject`

`AnyObject` is used when working with class types.

```swift
class Animal {
    var name: String
    init(name: String) {
        self.name = name
    }
}

class Dog: Animal {
    func bark() {
        print("Woof!")
    }
}

let objects: [AnyObject] = [Animal(name: "Lion"), Dog(name: "Fido")]

for object in objects {
    if let dog = object as? Dog {
        print("\(dog.name) is a dog.")
        dog.bark()
    } else if let animal = object as? Animal {
        print("\(animal.name) is an animal.")
    }
}
// Outputs:
// Lion is an animal.
// Fido is a dog.
// Woof!
```

---

## Practical Example: Polymorphism with Type Casting

Consider a media library with different types of media items.

```swift
class MediaItem {
    var title: String
    init(title: String) {
        self.title = title
    }
}

class Movie: MediaItem {
    var director: String
    init(title: String, director: String) {
        self.director = director
        super.init(title: title)
    }
}

class Song: MediaItem {
    var artist: String
    init(title: String, artist: String) {
        self.artist = artist
        super.init(title: title)
    }
}

let library: [MediaItem] = [
    Movie(title: "Inception", director: "Christopher Nolan"),
    Song(title: "Imagine", artist: "John Lennon"),
    Movie(title: "The Matrix", director: "The Wachowskis"),
    Song(title: "Bohemian Rhapsody", artist: "Queen")
]
```

### Iterating and Type Casting

```swift
for item in library {
    if let movie = item as? Movie {
        print("Movie: \(movie.title), directed by \(movie.director)")
    } else if let song = item as? Song {
        print("Song: \(song.title), by \(song.artist)")
    }
}
// Outputs:
// Movie: Inception, directed by Christopher Nolan
// Song: Imagine, by John Lennon
// Movie: The Matrix, directed by The Wachowskis
// Song: Bohemian Rhapsody, by Queen
```

**Explanation:**

- The `library` array contains `MediaItem` instances.
- Type casting with `as?` checks if each item is a `Movie` or `Song`.
- Downcasting allows access to subclass-specific properties.

---

## Forced Downcasting vs. Optional Downcasting

### When to Use Forced Downcasting (`as!`)

Use `as!` when you are certain about the type of an instance. However, this can lead to runtime errors if the assumption is wrong.

```swift
for item in library {
    let movie = item as! Movie
    print("Movie: \(movie.title), directed by \(movie.director)")
}
// Runtime Error if an item is not a Movie
```

**Note:** It's safer to use optional downcasting (`as?`) and handle the nil case.

### Using `as` for Upcasting

In some cases, you might need to upcast explicitly.

```swift
let movie = Movie(title: "Interstellar", director: "Christopher Nolan")
let mediaItem = movie as MediaItem // Upcasting to MediaItem
```

---

## Type Casting with `switch` Statements

Using a `switch` statement can make type checking more concise.

```swift
for item in library {
    switch item {
    case let movie as Movie:
        print("Movie: \(movie.title), directed by \(movie.director)")
    case let song as Song:
        print("Song: \(song.title), by \(song.artist)")
    default:
        print("Unknown media item")
    }
}
```

---

## Understanding the `Any` and `AnyObject` Types

### `Any`

- Can represent any type, including functions.
- Use when you need to work with heterogeneous data types.

### `AnyObject`

- Represents any class type.
- Useful when working with collections of class instances.

**Example:**

```swift
let mixedArray: [Any] = [42, "Hello", { (name: String) in "Hi, \(name)" }]

for element in mixedArray {
    if let function = element as? (String) -> String {
        print(function("Swift"))
    } else {
        print("Not a function")
    }
}
// Outputs:
// Not a function
// Not a function
// Hi, Swift
```

---

## Key Concepts and Terminology

- **Type Casting**: Treating an instance as if it were of a different type within its own class hierarchy.
- **Upcasting**: Casting a subclass instance to one of its superclass types.
- **Downcasting**: Casting a superclass instance to one of its subclass types.
- **`is` Operator**: Checks if an instance is of a certain type.
- **`as?` Operator**: Optional downcast; returns `nil` if the cast fails.
- **`as!` Operator**: Forced downcast; triggers a runtime error if the cast fails.
- **`Any` Type**: Can represent an instance of any type, including value and function types.
- **`AnyObject` Type**: Can represent an instance of any class type.

---

## Conclusion

Type casting is a powerful feature in Swift that allows you to check and interpret the type of an instance at runtime. By understanding how to use the `is`, `as?`, and `as!` operators, you can write flexible and safe code that handles different types dynamically.

Key takeaways:

- Use `is` to check an instance's type.
- Use `as?` for safe, optional downcasting.
- Use `as!` for forced downcasting when you're certain of the type.
- Upcasting is implicit but can be done explicitly with `as`.
- `Any` and `AnyObject` allow for working with heterogeneous collections.

---

## References

- [The Swift Programming Language - Type Casting](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html)
- [Swift Standard Library Reference - Any](https://developer.apple.com/documentation/swift/any)
- [Swift Standard Library Reference - AnyObject](https://developer.apple.com/documentation/swift/anyobject)

---

## Questions
1. What is type casting used for in Swift?
2. What are the `is` and `as` operators used for?
3. How does Swift's `is` operator work with class types?
4. What is the difference between upcasting and downcasting?
5. How does conditional downcasting with `as?` differ from forced downcasting with `as!`?
6. Why might you prefer to use `as?` over `as!`?
7. What could happen if you use `as!` and the cast fails?
8. What is the purpose of the `Any` type in Swift?
9. How is `AnyObject` different from `Any`?
10. How can you use a `switch` statement to check for specific types in an array of `Any`?
11. When would you use upcasting in Swift? (maybe difficult)
12. How does downcasting allow access to subclass-specific properties?
13. Why might you need to cast items in a collection with mixed types?
14. What is the role of `Any` in holding values of different types?
15. In what scenarios would you use `AnyObject`?
16. How does type casting support polymorphism in Swift?
17. Why is type checking useful when dealing with class hierarchies?
18. What happens if you try to downcast to a subclass that the instance does not belong to? (maybe difficult)
19. How can `Any` and `AnyObject` enhance the flexibility of collections in Swift? (maybe difficult)
20. What is one advantage of using `is` for type checking before attempting a downcast? 