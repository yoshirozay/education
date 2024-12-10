# What is Big O Notation?
Big O Notation is the language computer scientists use when comparing the performance of algorithims. It's all about dominant operations
  time (how fast)
  space (how much memory)

Big O Notation is benchmarked against the worst case scenario (the longest this algorithim will take).

There's typically a linear relationship between the amount of elements in an algorithim and its runtime, although it is not perfectly linear because computers are so fast now. 

Linear time is referred to as 0(n) and is present wherever there is a loop, where n is the time complexity based on the length of the object.

```swift
func linearTime(_ A: [Int]) -> Int {
    for i in 0..<A.count {
        if A[i] == 0 {
            return 0
        }
    }
    return 1
}
```

Constant Time, where the algorithm does a calculation and returns a value, this notation is 0(1) (extremely quick)

```swift
func constantTime(_ n: Int) -> Int {
    let result = n * n
    return result
}
```


Logaithmic Time, the algorithm loops and cuts the value in half each time (binary search tree)
```swift
func logarithmicTime(_ N: Int) -> Int {
    var n = N
    var result = 0
    while n > 1 {
        n /= 2
        result += 1
    }
    return result
}
```

Quadratic Time, the algorithm time doubles because of two for loops, with one embedded in eachother.

```swift
func quadratic(_ n: Int) -> Int {
    var result = 0
    for i in 0..<n {
        for j in i..<n {
            result += 1
            print("\(i) \(j)")
        }
    }
    return result
}
```
