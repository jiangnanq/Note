---
title: Summary of collections
date: 2017-6-28
tags: iOS
---

1. To iterate an array with Struct
  You cannot change property of struct in loop. During the loop, you are operate the copy of the struct. Old loop method should be used for it. 
```Swift
  for index in 0..<nearbyTrolleys.count {
      nearbyTrolleys[index].distance = nearbyTrolleys[index].location.distance(from: currentlocation)
  }
```

1. Check item exist in array
```Swift
  var b:[String] = ["a", "b", "c", "d", "e"]****
  b.contains("a")
```

1. Filter item in array
```Swift
  var a = [1, 2, 2, 3, 4, 5]
  let a3 = a.filter{$0 == 2}
  print(a3)
```

1. Sort array
```Swift
  var a = [1, 2, 2, 3, 4, 5]
  let d = a.sorted(by: >)
```

1. Map 
```Swift
  let a4 = [1,3,5,7]
  let b4 = a4.map { (item:Int) -> Int in
      return item * 2
  }
```

1. Reduce
```Swift
let status = [true, true, true, true]
var s1 = status.reduce(true) { (r, s) -> Bool in
  return r && s
}
```