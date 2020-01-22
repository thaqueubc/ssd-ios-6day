# iOS Development: A Brief Introduction to Swift

1. [ Installing XCode ](#1)
2. [ Writing Swift Correctly ](#2)
3. [ Swift Playgrounds ](#3)
4. [ Swift Types ](#4)
5. [ Constants and Variables ](#5)
6. [ Optionals ](#6)
7. [ Arrays, Sets and Dictionaries ](#7)
8. [ Loops ](#8)
9. [ Methods and Functions ](#9)
10. [ Tuples ](#10) 
11. [ Inheritance ](#11)
13. [ Enums ](#12)
14. [ Additional Resources ](#13)
15. [ In-class Assignment ](#14)

<a name="1"></a>
## 1) Installing XCode

Download XCode from here: https://developer.apple.com/downloads/
*You may need to create an Apple Id to create a developer account. Please create your developer account now.*

You can also use the app store (but this is often much slower)

*Please ensure you have the latest stable version of Xcode (which ships with Swift).
Open Xcode and in the main menu bar click Xcode -> About Xcode*

![](https://i.imgur.com/xX47YZN.png)


**If you need to upgrade...but have existing iOS projects that use previous versions of Swift, it is recommended that you keep both instances of XCode installed.
But for most of you who most likely do not have existing iOS projects, delete your current instance once you have the xip downloaded for the new version then install the new one.**

### Instructions for XCode Install IF Necessary

![](https://i.imgur.com/4vBnZiQ.png)

Click on the downloaded xip folder

![](https://i.imgur.com/2yDtwyv.png)

Open Xcode

![](https://i.imgur.com/O0MBO4Y.png)




<a name="2"></a>
## 2) Writing Swift Correctly

Some notes on style

- Use camel case
- Use upper case for types (`String`, `Int`, `MyClassName` etc.), lower case for everything else (`myVariable`, `anotherVariable` etc.)
- Use 2 spaces (not tabs) for indentation (navigate to XCode > Preferences > Text Editing > Indentation to change your settings)

![](https://i.imgur.com/EEkYl4r.png)

It's important to ensure consistency when writing any programming language. Using a style guide is a great tool for this purpose! See Ray Wenderlich's [Swift Style Guide](https://github.com/raywenderlich/swift-style-guide) for more detailed notes on how we'll be writing Swift during this course.

<a name="3"></a>
## 3) Swift Playgrounds

Open XCode and select "Get started with a playground".

![](https://i.imgur.com/VTKqmWS.png)

Select the "Blank" template.

![](https://i.imgur.com/WtME0yl.png)

Name your playground and save it in a convenient spot.

![](https://i.imgur.com/zGxrRlc.png)

<a name="4"></a>
## 4) Swift Types

### Basic Types

```swift
// Bool
let isRed: Bool = false

// String
let name: String = "Jane"

// Character
let myChar: Character: "a"

// Float
let someNum: Float = 5.0

// Double
let someMonaaay: Double = 5.00

// Note: Float can represent 32 bit floating point number, whereas Double can represent a 64 bit floating point number (and is thus more precise).

```

<a name="5"></a>
## 5) Constants and Variables

### `let`

In Swift we use the `let` keyword to declare a variable that is immutable (it can't be changed after it has been initialized).

```swift

let firstName = "Jane" // note that the type is inferred here

firstName = "John" // Can't do this!

```

### `var`

We use `var` to declare a variable that is mutable (its value can be changed or "mutated")

```swift

var firstName = "Jane"

firstName = "John" // This works!

```

### When to use `let` vs. `var`

If a stored value in your code will not be changing at any point, *always* declare it as a constant with the `let` keyword. Use `var` only to declare variables that you are sure will change. A good practice is to declare everything with `let` and then change to `var` as needed. The Swift compiler is able to optimize for best performance when we write code for immutablility first.

### Let's try out some code in our playground

What will be printed?

```Swift

let firstName: String = "Jane"

var lastName: String = "Jones"
lastName = "James"

print("Full Name: " + firstName + " " + lastName)

```

### Exercise:

Spend a few minutes declaring some variables using different types, and trying out `let` and `var` in your playground. Try mutating a variable declared with `let`. What happens?


<a href="#6"></a>
## 6) Optionals

In Swift, the Optional type is used if a variable will store either a value OR nil (no value). If a value is stored in an optional variable, you must unwrap the optional in order to access the value.

There are 2 ways to declare an optional

1) Explicitly

```swift
let possibleString: String? = "Hai thar"
```

2) Implicitly

```swift
let assumedString: String! = possibleString
```

Use implicitly unwrapped optionals ONLY for instance variables that you are sure will be initialized with a value prior to use (in a constructor for instance)

### Unwrapping Optionals

```swift

let possibleString: String? = "Hai thar"

// optional binding
if let anActualString = possibleString {
  // If the conditional evaluates to true, "Hai thar" is stored
  // in anActualString and can be used within the scope
  // of this block
  
  print(anActualString)
}


// another less swifty way (not preferred)

if possibleString != nil {
  print(possibleString!)
}

```
### Exercise

Paste the following code into your playground


```swift

let stringNum = "5"
let optionalNumber = Int(stringNum)

// If the value in stringNum was successfully cast to an integer, optionalNumber holds the value 5, nil otherwise

// In order to access the value of optionalNumber, you will need to unwrap it

if let anActualInteger = optionalNumber {
  // If the conditional evaluates to true, 5 is stored
  // in anActualInteger and can be used within the scope
  // of this block
  let aNewInt = anActualInteger + 10
  print(aNewInt)
} else {
  print("optionalNumber is nil")
}

```
Try changing the value of `stringNum` to something other than an integer.

### Force Unwrapping Optionals

```swift

let optionalString: String? = "Hai thar"

print(anOptionalString!)

```

You should be careful when force unwrapping an optional using `!`. Your code will compile, but if the optional ends up being nil during execution, you'll get a fatal error and your app will crash. Never force unwrap an optional unless your are sure that it will have a value during execution. This also applies to nil values in implicitly declared optionals.

### Exercise

Paste the following code into your playground. What happens?

```swift
var myString: String?
myString = nil

// This line compiles but will cause a fatal error during execution. Avoid force unwrapping optionals unless you can be sure they are not nil
print(myString!)

```

### Exercise

Paste the following code into your playground. Read through each line and play with the values. Try to add a `middleName` optional variable in your code.

```swift
// firstName is an explicit optional type: it can only be nil or a String and must be unwrapped
var firstName: String?

if firstName == nil {
  print("A first name has not been given.");
}

firstName = "Jane"

// firstName is unwrapped and the String value placed in localFirstName
// if firstName is nil the conditional evaluates to false
if let localFirstName = firstName {
  // localFirstName lives within the scope of the if block only
  print(localFirstName)
}

// lastName is an explicit optional type: it can only be nil or a String and must be unwrapped
var lastName: String?

lastName = "Jones"

// You can unwrap multiple optionals in the same conditional statement
if let localFirstName = firstName, let localLastName = lastName {
  print("Full Name: " + localFirstName + " " + localLastName)
}

lastName = nil

// The line below force unwraps an optional. Since the optional is nil, there will be a fatal error
print(lastName!)
```

<a name="7"></a>
## 7) Arrays, Sets and Dictionaries

### Arrays

Arrays in Swift are used to store ordered lists of the same type of value.

```swift
let firstNames: [String] = ["Sally", "Charlie", "Jane"]
```

### Sets

Sets in Swift are used to store unordered lists of the same type of value.

```swift
let firstNames: Set<String> = ["Sally", "Charlie", "Jane"]
```

A set cannot be depended on for maintaining an order. `firstNames` above, may be stored in memory like this: `["Charlie", "Sally", "Jane"]`

### Dictionaries

A dictionary in Swift stores associations between keys of the same type and values of the same type. Dictionaries have no defined ordering.

When you try to retrieve a value from a dictionary using a key, you will receive an optional. You will need to unwrap this optional to access the value (if it's not nil).

```swift
let userFirstNames: [Int: String] = [123: "Sally", 456: "Charlie", 987: "Jane"]

if let firstName = userFirstNames[123] {
  print(firstName)
}
```

<a name="8"></a>
## 8) Loops

### Looping Over Collections

```swift

for num in 1...5 {
  print(num)
}

// prints:
// 1
// 2
// 3
// 4
// 5

for _ in 1...5 {
  print("hai")
}

// prints:
// hai
// hai
// hai
// hai
// hai

```


Generally prefer `for` over `while` for accessing collections.

#### Arrays

```swift

let firstNames: [String] = ["Sally", "Charlie", "Jane"]

for name in firstNames {
  print(name)
}

// prints:
// Sally
// Charlie
// Jane

```

#### Sets

```swift

let firstNames: Set<String> = ["Sally", "Charlie", "Jane"]

for name in firstNames {
  print(name)
}

// prints:
// Charlie
// Jane
// Sally

// Note that values are no in order because we are using a set

```

#### Dictionaries

```swift

let userFirstNames: [Int: String] = [123: "Sally", 456: "Charlie", 987: "Jane"]

for (id, name) in userFirstNames {
  print(id, ": " + name)
}

// prints:
// 123 : Sally
// 456 : Charlie
// 987 : Jane

```

### Exercise (5-10 mins)

In your playground, create a dictionary of 4 country names that reference a population integer for each country. Add some sample data (ie. `"Canada": 30000000`). Loop through your dictionary and print the country name and its population.

<a name="9"></a>
## 9) Methods and Functions

### Functions

```swift

func printFullName(firstName: String, lastName: String) {
  print(firstName + " " + lastName)
}

```

Functions in Swift have named parameters, which must be used explicitly when calling a function.

```swift

// Note the String return value
func getFullName(firstName: String, lastName: String) -> String {
  let fullName = firstName + " " + lastName
  
  // Use return keyword explicitly
  return fullName
}

// Note the named parameters (firstName and lastName)
let fullName = getFullName(firstName: "Jane", lastName: "Jones")

print(fullName)

```

### Methods

Methods are functions that belong to a type.

```swift

struct Printer {
  func printName(name: String) {
    print(name)
  }
}

let printer = Printer()

printer.printName(name: "Sally")

// printName is a method of the Printer type

```

<a name="10"></a>
## 10) Tuples

Sometimes you might want to return multiple values from a function. You can do this using a tuple.

a tuple in Swift is a comma separated list of values.

```swift

func getFullName(firstName: String, lastName: String) -> String {
  let fullName = firstName + " " + lastName
  
  return fullName
}

// This function returns a tuple. Our tuple has named parameters id and fullName
func getUser(id: Int, firstName: String, lastName: String) -> (id: Int, fullName: String) {
  let fullName = getFullName(firstName: firstName, lastName: lastName)
  
  // return an (id, fullName) tuple
  return (id: id, fullName: fullName)
}

let user = getUser(id: 123, firstName: "Jane", lastName: "Jones")

print(user)

// prints:
// (id: 123, fullName: "Jane Jones")

```

<a name="11"></a>
## 11) Inheritance

In Swift, A class can inherit methods, properties, and other characteristics from another class. When one class inherits from another, the inheriting class is known as a subclass, and the class it inherits from is known as its superclass. Classes are the only type in Swift that has access to inheritance.


```swift

class Pet {
  var type: String
  var color: String
  var size: String
  
  init(type: String, color: String, size: String) {
    self.type = type
    self.color = color
    self.size = size
  }
  
  func getDescription() -> String {
    return size + ", " + color + " " + type
  }
}

// The Dog class inherits from the Pet class
class Dog: Pet {
  var breed: String
  
  init(breed: String, color: String, size: String) {
    self.breed = breed
    
    super.init(
      type: "dog",
      color: color,
      size: size
    )
  }
  
  override func getDescription() -> String {
    return size + ", " + color + ", " + breed + " " + type
  }
}

let gsd = Dog(breed: "german shepherd", color: "black", size: "large")

print(gsd.getDescription())

// prints:
// large, black, german shepherd dog


```

### Exercise (10 mins)

Paste the code above into your playground. Add another class for a different pet (like `Cat` or `Guinea Pig`)


<a name="12"></a>
## 12) Enums

Enum is short for Enumeration. An enum defines a common type for a group of related values. It allows you to work with those values in a type-safe way.

Enums are declared using the enum keyword and each value is declared using the case keyword.

Each enum in Swift is it's own type. See the `DogBreed` enum below.

```swift

class Pet {
  var type: String
  var color: String
  var size: String
  
  init(type: String, color: String, size: String) {
    self.type = type
    self.color = color
    self.size = size
  }
  
  func getDescription() -> String {
    return size + ", " + color + " " + type
  }
}

enum DogBreed: String {
  case goldenRetriever = "golden retriever"
  case germanShepherd = "german shepherd"
  case chihuahua = "chihuahua"
}

class Dog: Pet {
  // breed is of type DogBreed
  var breed: DogBreed
  
  init(breed: DogBreed, color: String, size: String) {
    self.breed = breed
    
    super.init(
      type: "dog",
      color: color,
      size: size
    )
  }
  
  override func getDescription() -> String {
    return size + ", " + color + ", " + breed.rawValue + " " + type
  }
}

let gsd = Dog(breed: DogBreed.germanShepherd, color: "black", size: "large")

print(gsd.breed.rawValue)

// prints:
// german shepherd

```

### Exercise (10 mins)

Paste the code above into your playground. Add enums for color and size and apply them in the Pet class.


<a name="13"></a>
## 13) Additional Resources

* [Swift Source Code on Github](https://github.com/apple/swift)
* [Swift Official Documentation](https://swift.org/)
* [Ray Wenderlich's Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)
* [WWDC 2019 Videos](https://developer.apple.com/videos/wwdc2019)

<a name="14"></a>
## 14) Assignment

Create an employee management system in your playground that does the following:

1) An Employee class, where each employee has an id, a name, an email address (an optional as not every employee has one), an employee type (ie. "contract", or "full time" etc.) and an employee status (ie. "active" or "inactive")

2) An EmployeeManager class, that can do the following:
    * Maintain a record of employees (can add new employees, and remove old ones)
    * Get the name of an employee, given an id
    * Get the email address of an employee, given an id
    * Get the employee type of an employee, given an id
    * Get the employee status of an employee, given an id
    * Print a list of the names of all employees

3) Test your implementation by: 
    * adding at least 5 Employees to your EmployeeManager
    * print a list of all employee names
    * call each EmployeeManager "get method" at least once
    * remove 3 Employees from the EmployeeManager
    * print a new list of all employee names

### Assignment Learning Outcomes

* Student can apply the correct Swift syntax
* Student can apply the correct Swift style (proper indentation etc.)
* Student can apply Swift types correctly
* Student code can fulfill the above outlined expectations (ie. your code works)
