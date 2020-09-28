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

```swift 
```

## Creating a frequency dictionary 

```swift 
```

#### Practice 

<details>
  <summary>Solution</summary> 
  
```swift 
```
  
</details> 

## Tranforming a dictionary 

```swift 
```

## `updateValue(:_, forKey:_)`

```swift 
var dict = ["iOS": "Obj-C", "android" : "Java" ]


if let oldValue = dict.updateValue("javascript", forKey: "web") {
  print("\(oldValue) was used for iOS progrmming")
} else {
  print("no value existed before")
}

let newValue = dict["iOS"] ?? ""

let webValue = dict["web"] ?? ""


print("new language is \(newValue)")

print("new language for web \(webValue)")
```

## Challenges 

#### Challenge 1 - Occurences of n or more 

MARK: Question 2 INCOMPLETE
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

