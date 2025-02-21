## Introduction to Objective-C

Objective-C is a general-purpose, object-oriented programming language that enhances the C programming language with Smalltalk-style messaging. It served as the primary language for macOS and iOS development until Swift's introduction, but it remains relevant for legacy code and specific use cases.

---

## Key Concepts

### 1. Syntax and Structure

- **Header and Implementation Files**:
    
    - Header files (`.h`) declare the interface.
    - Implementation files (`.m`) define the functionality.
    
    ```objc
    // MyClass.h
    @interface MyClass : NSObject
    - (void)greet;
    @end
    
    // MyClass.m
    @implementation MyClass
    - (void)greet {
        NSLog(@"Hello, World!");
    }
    @end
    ```
    

### 2. Memory Management

- **Manual Retain-Release (MRR)**:
    - Memory is manually managed using `retain`, `release`, and `autorelease`.
- **Automatic Reference Counting (ARC)**:
    
    - Introduced to simplify memory management by automating object lifecycle handling.
    
    ```objc
    NSString *message = [[NSString alloc] initWithFormat:@"Hello, %@!", @"Objective-C"];
    NSLog(@"%@", message);
    // ARC eliminates the need for explicit `release` calls.
    ```
    

### 3. Messaging

- **Dynamic Method Invocation**:
    
    - Methods are invoked dynamically at runtime using messages.
    
    ```objc
    [object performSelector:@selector(methodName)];
    ```
    

### 4. Properties

- **Declaring Properties**:
    
    - Streamlines the creation of getter and setter methods.
    
    ```objc
    @property (nonatomic, strong) NSString *name;
    ```
    
- **Synthesizing Properties**:
    
    - Automatically generates getter and setter implementations.
    
    ```objc
    @synthesize name;
    ```
    

### 5. Categories and Extensions

- **Categories**:
    
    - Extend existing classes by adding methods without subclassing.
    
    ```objc
    @interface NSString (Reverse)
    - (NSString *)reverseString;
    @end
    ```
    
- **Extensions**:
    - Allow private methods or properties to be added to a class.

### 6. Protocols

- **Objective-C Protocols**:
    
    - Define a blueprint of methods that conforming classes must implement.
    
    ```objc
    @protocol MyProtocol <NSObject>
    - (void)doSomething;
    @end
    
    @interface MyClass : NSObject <MyProtocol>
    @end
    ```
    

---

## Sample Program

```objc
#import <Foundation/Foundation.h>

@interface Greeter : NSObject
@property (nonatomic, strong) NSString *greeting;
- (void)sayHello;
@end

@implementation Greeter
- (void)sayHello {
    NSLog(@"%@", self.greeting);
}
@end

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Greeter *greeter = [[Greeter alloc] init];
        greeter.greeting = @"Hello, Objective-C!";
        [greeter sayHello];
    }
    return 0;
}
```

---

## Summary

Objective-C remains a critical language for maintaining legacy iOS and macOS projects. Its dynamic nature and compatibility with C make it versatile, while understanding its basics equips developers to work with existing Objective-C codebases or transition to Swift effectively.

---
