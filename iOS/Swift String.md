# Summary of Swift time operation

1. Trim alphabet from string

```swift
let b1 = "243W"
let a1 = Int(b1.trimmingCharacters(in: CharacterSet(charactersIn: "01234567890.").inverted))
```
