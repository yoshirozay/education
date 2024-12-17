## What is a Fibonacci series?
1,1,2,3,5,8,13,21...

f = fib(n-1) + fib(n-2)

Series of numbers where every number, after the first two, is the sum of the two preceding ones.

This sequence shows up over and over again throughout nature (golden ratio, flowers, space)

This pattern is also very useful for stock predictions.

```swift
func fibNaive(_ n: Int) -> Int {
    print(n)
    if n == 0 {
        return 0
    } else if n == 1 {
        return 1
    } else {
        return fibNaive(n - 1) + fibNaive(n - 2)
    }
}

fibNaive(20) // 20 = 13s / 22 = 54 s
```
