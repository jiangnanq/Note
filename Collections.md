# Summary of collections

1. To iterate an array with Struct
  You cannot change property of struct in loop. During the loop, you are operate the copy of the struct. Old loop method should be used for it. 
  ```Swift
    for index in 0..<nearbyTrolleys.count {
        nearbyTrolleys[index].distance = nearbyTrolleys[index].location.distance(from: currentlocation)
    }
  ```

2. Check item exist in array
  ```Swift
    var b:[String] = ["a", "b", "c", "d", "e"]
    b.contains("a")
  ```

3. Filter item in array
  ```Swift
    var a = [1, 2, 2, 3, 4, 5]
    let a3 = a.filter{$0 == 2}
    print(a3)
  ```

4. Sort array
  ```Swift
    var a = [1, 2, 2, 3, 4, 5]
    let d = a.sorted(by: >)
  ```

5. Map 
  ```Swift
    let a4 = [1,3,5,7]
    let b4 = a4.map { (item:Int) -> Int in
        return item * 2
    }
  ```

6. Reduce
  ```Swift
  let status = [true, true, true, true]
  var s1 = status.reduce(true) { (r, s) -> Bool in
    return r && s
  }
  ```