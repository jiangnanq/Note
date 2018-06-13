# Summary of Swift time operation

1. **Get seconds since today midnight**
```Swift
let t = Calendar.current.startOfDay(for: Date())
let d = Date()
let e = Int(d.timeIntervalSince(t))
```
