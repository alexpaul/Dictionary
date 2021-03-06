# Dictionary

Swift's Dictionary. A dictionary is a collection of key, value pairs. The `key` is required to conform to the `Hashable` protocol.

```swift 
struct Dictionary<Key, Value> where Key: Hashable
```

> Apple documentation: A dictionary is a type of hash table, providing fast access to the entries it contains. Each entry in the table is identified using its key, > which is a hashable type such as a string or number. You use that key to retrieve the corresponding value, which can be any object. In other languages, similar data types are known as hashes or associated arrays.

> Recall: Hash table is an abstract data type. 

<details>
  <summary>Hash Table</summary> 
  
[YouTube - Hash Table Implementation](https://www.youtube.com/watch?v=58GbN9iBZWM)
  
```swift 
import UIKit

//
var buckets = Array(repeating: 0, count: 2)

// hashValue is a built-in hash function
// returns a hash value for a key
// it's possible to get a negative number
// how can we fix this - take the absolute value of the operation
let alexIndex = abs("Alex".hashValue % buckets.count)
let brendonIndex = abs("Brendon".hashValue % buckets.count)
let ahadIndex = abs("Ahad".hashValue % buckets.count)
let tanyaIndex = abs("Tanya".hashValue % buckets.count)

print("goes in \(alexIndex) index")
print("goes in \(brendonIndex) index")
print("goes in \(ahadIndex) index")
print("goes in \(tanyaIndex) index")


var dict = [String: Int]()
dict["Sweden"] = 1


// Implemenet Hash Table
// e.g HashTable<String, Int>(capacity: 4)
struct HashTable <Key: Hashable, Value> {
  // (key, value) e.g "Tiffany": 21
  private typealias Element = (key: Key, value: Value)
  
  // collision resolution being implemented using chaining
  private typealias Bucket = [Element] // this represent the chains
  
  private var buckets: [Bucket]
  
  private (set) var count = 0 // getter is public, setter is private
  
  init(capacity: Int) {
    assert(capacity > 0) // crashes if not
    buckets = Array<Bucket>(repeating: [], count: capacity)
    // e.g buckets = [[], [], [(key: "Tiffany": 21)], []]
  }
  
  // method to return index where key will be stored
  func index(forKey key: Key) -> Int {
    return abs(key.hashValue % buckets.count)
  }
  
  // method to search for a value given a key
  func value(forKey key: Key) -> Value? {
    let index = self.index(forKey: key)
    for element in buckets[index] {
      if element.key == key {
        return element.value
      }
    }
    return nil
  }
  
  // method to update a value for a given key
  mutating func update(value: Value, forKey key: Key) -> Value? {
    let index = self.index(forKey: key)
    for (i, element) in buckets[index].enumerated() {
      if element.key == key {
        let oldValue = element.value
        // update the current value
        buckets[index][i].value = value
        return oldValue
      }
    }
    // we get here if there's no value
    buckets[index].append((key: key, value: value))
    count += 1
    return nil // to signify there wasn't an existing value
  }
  
  // method to remove an element at a given key
  mutating func removeValue(forKey key: Key) -> Value? {
    let index = self.index(forKey: key)
    for (i, element) in buckets[index].enumerated() {
      if element.key == key {
        buckets[index].remove(at: i)
        count -= 1
        return element.value
      }
    }
    return nil
  }
  
  // we can have multiple subscipt methods taking in varied arguments
  subscript(key: Key) -> Value? {
    get {
      return value(forKey: key)
    } set {
      if let value = newValue {
        update(value: value, forKey: key)
      } else {
        removeValue(forKey: key)
      }
    }
  }
}

// test the hash table
// key is String and the value is an Int and capacity is 4
var hashTable = HashTable<String, Int>(capacity: 4)

hashTable["Tiffany"] = 21
//hashTable.update(value: 21, forKey: "Tiffany")
hashTable.update(value: 25, forKey: "Eric")

hashTable.count

print(hashTable)

//hashTable.removeValue(forKey: "Tiffany")
hashTable["Tiffany"] = nil

print(hashTable.count) // 1
print(hashTable)

// optional binding
if let age = hashTable["Alex"] {
  print("\(age) exist")
} else {
  print("does not exist")
}

// nil coalescing
let age = hashTable["Cameron"] ?? 100
print(age)
```
</details> 

## 1. Creating a dictionary 

```swift 
var capitals = [String: String]() // initializer syntax 
```

```swift 
var cohorts = ["iOS": [6.1, 6.3], "web": [6.2, 6.4]] // dictionary literal 
```

## 2. Iterating over a dictionary 

```swift 
var cohorts = ["iOS": [6.1, 6.3], "web": [6.2, 6.4]]

for (stack, classes) in cohorts {
  print("\(stack) has \(classes.count) classes: \(classes)")
}
/*
web has 2 classes: [6.2, 6.4]
iOS has 2 classes: [6.1, 6.3]
*/
```

## 3. Runtime operations on a dictionary 

| Operation | Runtime |
|:----:|:-----:|
| Search | O(1) |
| Insertion | O(1) |
| Deletion | O(1) |


```swift 
var dict = ["September": ["Labor Day"], "October" : ["Columbus Day"], "November" : ["Thanksgiving Day"]]

// search
if let holidays = dict["September"] { // O(1)
  print(holidays)
}

// insertion
dict["November"]?.append("Veterans Day") // O(1)

print("dictionary after insertion: \(dict)")

// deletion
dict["October"] = nil // O(1)

print("dictionary after deletion: \(dict)")
```

## 4. Creating a frequency dictionary 

```swift 
var freqDict = [String: Int]()

let languages = ["Javascript","Swift","Python","C++","Javascript","Python","C++","Javascript","C++","Python","Javascript","Swift","Javascript"]

for language in languages {
  if let count = freqDict[language] {
    freqDict[language] = count + 1
  } else {
    freqDict[language] = 1
  }
}

print(freqDict) // ["Javascript": 5, "C++": 3, "Swift": 2, "Python": 3]
```

## 5. `default` value 

Use `default` if you rather using a prescribed value as opposed to `nil`

```swift 
var allowances = ["Miles": 10, "Norah": 10]

print(allowances["Miles", default: 0]) // 10

print(allowances["Alex", default: 0]) // 0
```

## 6. Refactor our creating of a frequency dictionary using `default` value

```swift 
var freqDict = [String: Int]()
let languages = ["Javascript","Swift","Python","C++","Javascript","Python","C++","Javascript","C++","Python","Javascript","Swift","Javascript"]

for language in languages {
  freqDict[language, default: 0] += 1
}

print(freqDict) // ["Swift": 2, "Python": 3, "C++": 3, "Javascript": 5]
```

## 7. Tranforming a dictionary 

#### `mapValues((Value) -> T)`

> Apple documentation: Returns a new dictionary containing the keys of this dictionary with the values transformed by the given closure.

```swift 
let tranformedDict = freqDict.mapValues { count -> String in
  if count > 2 {
    return "Popular"
  } else {
    return "Not Popular"
  }
}

print(tranformedDict) // ["C++": "Popular", "Swift": "Popular", "Javascript": "Popular", "Cobol": "Not Popular", "Python": "Popular"]
```

#### `compactMapValues((Value) -> T?)`

> Apple documentation: Returns a new dictionary containing only the key-value pairs that have non-nil values as the result of transformation by the given closure.

```swift 
let classAttendance = ["Rachel": nil, "James": 85, "Heather": 90, "Tim": nil, "Esther": nil, "Robert": 75]

let availableAttendance = classAttendance.compactMapValues { $0 }

print(availableAttendance) // ["Heather": 90, "James": 85, "Robert": 75]
```

## 8. `updateValue(:_, forKey:_)`

Use `updateValue(:_, forKey:_)` if you need to know whether there was a previous value when updating the value for a key. 

```swift 
var dict = ["iOS": "Objective-C", "Android" : "Java" ]

if let oldValue = dict.updateValue("Swift", forKey: "iOS") {
  print("old valus was \(oldValue)")
} else {
  print("no value existed before")
}
```

## 9. Built-in types that are similar to dictionary 

* UserDefaults
* NSCache 

## 10. Be able to perform the following operations for understanding 

CRUD - Create, Read, Update, Delete, Search

## Runtime vs Compile time errors 

#### Runtime error 

```swift 
var cohorts = ["iOS": [6.1, 6.3], "web": [6.2, 6.4], "iOS": [1.0]] // [String: Double]
// key duplication is a runtime error: Fatal error: Dictionary literal contains duplicate keys: file Swift/Dictionary.swift, line 826
```

#### Compile time error 

```swift 
var people = [Person: Int]() // compile time error 
```

## 11. Create a dictionary grouping from a given array

Using the [`init(grouping:by:)`](https://developer.apple.com/documentation/swift/dictionary/3127163-init) initializer we can pass in a given closure and an array and get back a dictionary where for example below, the keys are the `gender` and the values are an array of people categorized by that given `gender`. 


Below we have a Person object and a created array people `[Person]`

```swift 
struct Person {
  let name: String
  let gender: String
}

extension Person {
  static var people: [Person] {
    return [
      Person(name: "Alex", gender: "Male"),
      Person(name: "Kim", gender: "Female"),
      Person(name: "Robert'", gender: "Male"),
      Person(name: "Tom", gender: "Male"),
      Person(name: "James", gender: "Male"),
      Person(name: "Tisha", gender: "Female"),
      Person(name: "Allison", gender: "Female"),
      Person(name: "Jake", gender: "Male"),
      Person(name: "Heather", gender: "Female"),
      Person(name: "Rachel", gender: "Female"),
      Person(name: "Cindy", gender: "Female")
    ]
  }
}
```

Using the dictionary initializer `init(grouping:by:)` we get back a dictionary of type `[String: [Person]]`

```swift 
let peopleDict = Dictionary(grouping: Person.people, by: { $0.gender }) // [String : [Person]]

for (gender, people) in peopleDict {
  print("====== \(gender) ======")
  print(people)
  print("\n")
}

/*
====== Female ======
[__lldb_expr_33.Person(name: "Kim", gender: "Female"), __lldb_expr_33.Person(name: "Tisha", gender: "Female"), __lldb_expr_33.Person(name: "Allison", gender: "Female"), __lldb_expr_33.Person(name: "Heather", gender: "Female"), __lldb_expr_33.Person(name: "Rachel", gender: "Female"), __lldb_expr_33.Person(name: "Cindy", gender: "Female")]


====== Male ======
[__lldb_expr_33.Person(name: "Alex", gender: "Male"), __lldb_expr_33.Person(name: "Robert\'", gender: "Male"), __lldb_expr_33.Person(name: "Tom", gender: "Male"), __lldb_expr_33.Person(name: "James", gender: "Male"), __lldb_expr_33.Person(name: "Jake", gender: "Male")]
*/
```


## 12. Challenges 

#### Challenge 1 - Numbers appearing n or more times in an array.

Write a function that takes in an array of integers (arr) and a number (n)
You function should return an array with only numbers appearing n or more times.
Your solution must work in O(n) time.

Example:
Input: [1,3,4,1,9,1,3,4,3,1,2], 3
Output: [1,3]

#### Challenge 2 - How many numbers are smaller that the current number

[LeetCode](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/)

#### Challenge 3 - Find Words That Can Be Formed by Characters

[LeetCode](https://leetcode.com/problems/find-words-that-can-be-formed-by-characters/)

#### Challenge 4 - Design HashMap 

[LeetCode](https://leetcode.com/problems/design-hashmap/)

#### Challenge 5 - Group Anagrams 

[LeetCode](https://leetcode.com/problems/group-anagrams/)

## Resources 

1. [Apple Documentation - dictionary](https://developer.apple.com/documentation/swift/dictionary)
2. [Swift Programming Guide - Collection Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html)

