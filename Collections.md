---
title: Summary of collections
date: 2017-6-28
tags: iOS
---

# Summary of collections

The summary of collections. 
Swift version: 3.0
Xcode version: 8.2.1

1. To iterate an array with Struct
  You cannot change property of struct in loop. During the loop, you are operate the copy of the struct. Old loop method should be used for it. 
  {% codeblock lang:swift %}
    for index in 0..<nearbyTrolleys.count {
        nearbyTrolleys[index].distance = nearbyTrolleys[index].location.distance(from: currentlocation)
    }
  {% endcodeblock %}

2. Check item exist in array
  {% codeblock lang:swift %}
    var b:[String] = ["a", "b", "c", "d", "e"]****
    b.contains("a")
  {% endcodeblock %}

3. Filter item in array
  {% codeblock lang:swift %}
    var a = [1, 2, 2, 3, 4, 5]
    let a3 = a.filter{$0 == 2}
    print(a3)
  {% endcodeblock %}

4. Sort array
  {% codeblock lang:swift %}
    var a = [1, 2, 2, 3, 4, 5]
    let d = a.sorted(by: >)
  {% endcodeblock %}

5. Map 
  {% codeblock lang:swift %}
    let a4 = [1,3,5,7]
    let b4 = a4.map { (item:Int) -> Int in
        return item * 2
    }
  {% endcodeblock %}

6. Reduce
  {% codeblock lang:swift %}
  let status = [true, true, true, true]
  var s1 = status.reduce(true) { (r, s) -> Bool in
    return r && s
  }
  {% endcodeblock %}