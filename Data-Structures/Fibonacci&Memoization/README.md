# Fibonacci Series Implementation

## What is a Fibonacci Series?
A Fibonacci sequence is a series of numbers where each number is the sum of the previous two numbers:
1, 1, 2, 3, 5, 8, 13, 21...

The mathematical formula is:
```
fn = f(n-1) + f(n-2)
```

This sequence appears frequently in nature:
- Golden ratio
- Flower petal arrangements
- Spatial patterns
- Stock market predictions

## Naive Implementation
This is the basic recursive implementation, which is highly inefficient:

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

// Example usage:
// fibNaive(20) // Takes about 13 seconds
// fibNaive(22) // Takes about 54 seconds
```

### Performance Issues
The naive implementation has exponential time complexity because:
- Numbers are recalculated multiple times
- Each recursive call spawns two more calls
- Computation time grows exponentially with input size

## Optimized Implementation with Memoization
Memoization is an optimization technique that:
- Stores previously calculated results
- Returns cached results when the same calculation is needed
- Reduces time complexity from exponential to O(n) (Linear Time)

```swift
// Cache for storing calculated Fibonacci numbers
var memo = [Int: Int]()

func fib(_ n: Int) -> Int {
    // Base cases
    if n == 0 { return 0 }
    else if n == 1 { return 1 }
    
    // Check if result is already calculated
    if let result = memo[n] { return result }
    
    // Calculate and store result
    memo[n] = fib(n - 1) + fib(n - 2)
    return memo[n]!
}

// Example usage:
// fib(22) // Calculates instantly
// Can handle up to fib(70) before integer overflow
```

### Performance Comparison
- Naive Implementation (fibNaive):
  - n=20: ~13 seconds
  - n=22: ~54 seconds
  
- Memoized Implementation (fib):
  - n=22: instant calculation
  - Can efficiently calculate up to n=70 (limited by integer size, not performance)
