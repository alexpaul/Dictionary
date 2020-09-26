# Dictionary

Swift's Dictionary. A dictionary is a collection of key, value pairs. The `key` is required to conform to the `Hashable` protocol.

```swift 
struct Dictionary<Key, Value> where Key: Hashable
```

> Apple documentation: A dictionary is a type of hash table, providing fast access to the entries it contains. Each entry in the table is identified using its key, > which is a hashable type such as a string or number. You use that key to retrieve the corresponding value, which can be any object. In other languages, similar data types are known as hashes or associated arrays.

> Recall: Hash table is an abstract data type. 


## Creating a dictionary 

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
