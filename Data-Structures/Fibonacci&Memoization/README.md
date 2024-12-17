## What is a Fibonacci series?
1,1,2,3,5,8,13,21...

fn = f(n-1) + f(n-2)

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

As you calculate higher and higher order of numbers, the algorithm takes longer and longer (exponentially) grows. This is a very, very expensive algorithm, so how can we make it really fast? This is where an important topic comes in, called Memoization.

## Memoization

To understand Memoization, it's useful to understand what Fibonacci struggles with. Numbers are recalculated over and over again.

Memoization is an optimization technique that stores expensive calculated results and returns them when asked for again. It's like caching expensive results. This process reduces the Big O Notation from exponential to O(n) Linear Time!

```swift
fibNaive(20) // 20 = 13s / 22 = 54 s

var memo = [Int: Int]()

func fib(_ n: Int) -> Int {
    if n == 0 { return 0}
    else if n == 1 { return 1 }

    if let result = memo[n] { return result }

    memo[n] = fib(n - 1) + fib(n - 2)

    return memo[n]!
}

fib(22) // 70 max
```
