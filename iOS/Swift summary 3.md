##Swift summary

1. Random value

```swift
let random = Int(arc4random_uniform(UInt32(mrtStations.count)))
astation  = mrtStations[random]
```

2. Remove alphabet from string

```swift
let a1 = Int(b1.trimmingCharacters(in: CharacterSet(charactersIn: "01234567890.").inverted))
```

3. Check seconds from today midnight

```swift
let t = Calendar.current.startOfDay(for: Date())
let d = Date()
let e = Int(d.timeIntervalSince(t))
```
