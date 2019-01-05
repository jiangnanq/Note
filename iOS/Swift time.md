## Swift time operation

1. Get seconds since today midnight

```swift
let t = Calendar.current.startOfDay(for: Date())
let d = Date()
let e = Int(d.timeIntervalSince(t))
```
2. Convert Date to String

```swift
var msg = ""
let dateformatter = DateFormatter()
dateformatter.dateFormat = "HH:mm:ss"
msg = msg + dateformatter.string(from: timestamp) 
```

3. Convert time difference to String

```swift
let ct = Date()
var ts = ""
var ms = ""
var ss = ""
if a.alarmStatus {
    let components = Calendar.current.dateComponents([.minute, .second], from: a.alarmtimestamp, to: ct)
    ms = "\(components.minute ?? 0):"
    ss = "\(components.second ?? 0)"
    ts = ms + ss
}
cell.bedLabel.text = ts
```

4. Check current time and call function

```swift
if Calendar.current.component(.minute, from: Date()) == 0
    && Calendar.current.component(.second, from: Date()) < 5
    && turningClock.contains(Calendar.current.component(.hour, from: Date())) {
    NotificationCenter.default.post(name: strokeBedNotification, object: nil)
}
```

5. Get weekday of a date

```swift
let day = Date()
let calendar = Calendar(identifier: .gregorian)
let wd = calendar.component(.weekday, from: day)
```
