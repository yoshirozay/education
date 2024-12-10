# What is Big O Notation?

Big O Notation is the language computer scientists use when comparing the performance of algorithms. It's all about dominant operations:
* Time (how fast)
* Space (how much memory)

Big O Notation is benchmarked against the worst case scenario (the longest this algorithm will take).

There's typically a linear relationship between the amount of elements in an algorithm and its runtime, although it is not perfectly linear because computers are so fast now. 

## Linear Time - O(n)
Linear time is referred to as O(n) and is present wherever there is a loop, where n is the time complexity based on the length of the object.

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
## Constant Time - 0(1)
Constant Time, where the algorithm does a calculation and returns a value, this notation is O(1) (extremely quick)

```swift
func constantTime(_ n: Int) -> Int {
    let result = n * n
    return result
}
```
## Logarithmic Time - O(log n)
Logarithmic Time, the algorithm loops and cuts the value in half each time (binary search tree, extremely fast)

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
## Quadratic Time - O(n²)
Quadratic Time, the algorithm time doubles because of two for loops, with one embedded in each other. (very slow)

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

When you embed one loop in another as you do with Quadratic Time, you will still get the correct answer / code that works, but it won't be performative. Quadratic is bad, Linear is okay, Logarithmic and Constant are good.

## Space Time Tradeoff
How do you improve a quadratic time algorithm? By adding more space. Creating another item to help improve the algorithm ultimately increases space (memory). Some items are 0(1) complexity (variables) while others are 0(n) complexity (arrays). Data Structures & Algos is about managing this tradeoff.
