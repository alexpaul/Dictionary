# Dictionary

Swift's Dictionary. A dictionary is a collection of key, value pairs. The `key` is required to conform to the `Hashable` protocol.

```swift 
struct Dictionary<Key, Value> where Key: Hashable
```

> Apple documentation: A dictionary is a type of hash table, providing fast access to the entries it contains. Each entry in the table is identified using its key, > which is a hashable type such as a string or number. You use that key to retrieve the corresponding value, which can be any object. In other languages, similar data types are known as hashes or associated arrays.

> Recall: Hash table is an abstract data type. 

<details>
  <summary>Hash Table</summary> 
  
```swift 
```

</details> 


## Creating a dictionary 

```swift 
var capitals = [String: String]() // initializer syntax 
```

```swift 
var cohorts = ["iOS": [6.1, 6.3], "web": [6.2, 6.4]] // dictionary literal 
```

## Iterating over a dictionary 

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

## Runtime operations on a dictionary 

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

## Creating a frequency dictionary 

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


## Tranforming a dictionary 

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

## `updateValue(:_, forKey:_)`

Use `updateValue(:_, forKey:_)` if you need to know whether there was a previous value when updating the value for a key. 

```swift 
var dict = ["iOS": "Objective-C", "Android" : "Java" ]

if let oldValue = dict.updateValue("Swift", forKey: "iOS") {
  print("old valus was \(oldValue)")
} else {
  print("no value existed before")
}
```

## Challenges 

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

