# Swift Networking: Understanding JSON, API Calls, and URLSession

## Introduction to JSON in Swift

JSON (JavaScript Object Notation) serves as a lightweight data interchange format that's both human-readable and machine-parseable. In Swift, we work with JSON data through encoding and decoding processes, transforming between JSON and Swift objects.

### Understanding JSON Structure

Let's start with a simple example of JSON data:

```json
{
    "name": "John Doe",
    "age": 30,
    "email": "john@example.com",
    "hobbies": ["reading", "hiking", "photography"],
    "address": {
        "street": "123 Main St",
        "city": "San Francisco",
        "country": "USA"
    }
}
```

To work with this JSON in Swift, we create matching data structures using `Codable`:

```swift
// Define our Swift structures to match the JSON structure
struct Person: Codable {
    let name: String
    let age: Int
    let email: String
    let hobbies: [String]
    let address: Address
}

struct Address: Codable {
    let street: String
    let city: String
    let country: String
}

// Example of decoding JSON
let jsonData = // ... JSON data from an API ...
do {
    let person = try JSONDecoder().decode(Person.self, from: jsonData)
    print("Name: \(person.name), Age: \(person.age)")
} catch {
    print("Decoding error: \(error)")
}
```

### Working with Custom Keys

Sometimes JSON keys don't match Swift naming conventions. We can handle this using `CodingKeys`:

```swift
struct User: Codable {
    let firstName: String
    let lastName: String
    let emailAddress: String
    
    enum CodingKeys: String, CodingKey {
        case firstName = "first_name"
        case lastName = "last_name"
        case emailAddress = "email"
    }
}
```

## Making API Calls with URLSession

URLSession is Swift's built-in networking framework. Let's explore how to use it effectively.

### Basic GET Request

```swift
func fetchData() {
    // 1. Create the URL
    guard let url = URL(string: "https://api.example.com/data") else {
        print("Invalid URL")
        return
    }
    
    // 2. Create the URLSession task
    let task = URLSession.shared.dataTask(with: url) { (data, response, error) in
        // 3. Handle the result
        if let error = error {
            print("Error: \(error.localizedDescription)")
            return
        }
        
        // 4. Check for valid response
        guard let httpResponse = response as? HTTPURLResponse,
              (200...299).contains(httpResponse.statusCode) else {
            print("Invalid response")
            return
        }
        
        // 5. Handle the data
        if let data = data {
            do {
                let decoder = JSONDecoder()
                let result = try decoder.decode(ResponseType.self, from: data)
                // Handle successful result
            } catch {
                print("Decoding error: \(error)")
            }
        }
    }
    
    // 6. Start the task
    task.resume()
}
```

### Making POST Requests

```swift
func postData(user: User) {
    guard let url = URL(string: "https://api.example.com/users") else { return }
    
    // 1. Create the request
    var request = URLRequest(url: url)
    request.httpMethod = "POST"
    request.setValue("application/json", forHTTPHeaderField: "Content-Type")
    
    // 2. Encode the data
    do {
        let encoder = JSONEncoder()
        request.httpBody = try encoder.encode(user)
    } catch {
        print("Encoding error: \(error)")
        return
    }
    
    // 3. Create and start the task
    let task = URLSession.shared.dataTask(with: request) { data, response, error in
        // Handle response similar to GET request
    }
    task.resume()
}
```

## Best Practices and Tips

### 1. Error Handling

Always implement comprehensive error handling:

```swift
enum APIError: Error {
    case invalidURL
    case networkError(Error)
    case invalidResponse
    case decodingError(Error)
    case serverError(statusCode: Int, message: String?)
}
```

### 2. Request Timeout

Configure appropriate timeouts for your requests:

```swift
let configuration = URLSessionConfiguration.default
configuration.timeoutIntervalForRequest = 30  // 30 seconds
configuration.timeoutIntervalForResource = 300 // 5 minutes
let session = URLSession(configuration: configuration)
```

### 3. Response Caching

Implement caching when appropriate:

```swift
let configuration = URLSessionConfiguration.default
configuration.requestCachePolicy = .returnCacheDataElseLoad
configuration.urlCache = URLCache(
    memoryCapacity: 10 * 1024 * 1024,    // 10 MB
    diskCapacity: 50 * 1024 * 1024       // 50 MB
)
```

### 4. Authentication

Handle authentication tokens:

```swift
func addAuthenticationToken(to request: inout URLRequest) {
    request.setValue("Bearer \(accessToken)", forHTTPHeaderField: "Authorization")
}
```
