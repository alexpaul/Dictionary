# Dictionary

Swift's Dictionary.


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
