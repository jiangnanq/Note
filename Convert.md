# All about convert (date, string, data)

1. Convert Date to String
```Swift
var msg = ""
let dateformatter = DateFormatter()
dateformatter.dateFormat = "HH:mm:ss"
msg = msg + dateformatter.string(from: timestamp) 
```

2. Convert time difference to String
```Swift
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
