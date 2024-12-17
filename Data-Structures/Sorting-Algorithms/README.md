## Bubble Sort
Sorts the array from least to greatest by moving the largest numbers to the end of the array. Starts by comparing the first number to the number on the right. It takes the greater of the two numbers, and repeats the comparison process all the way down the array until the greatest number is at the end (right) of the array.

Big-O-Notation is O(N^2)

```swift
class BubbleSort {
    func sort(_ array: [Int]) -> [Int] {
        var arr = array
        let n = arr.count
        for i in 0..<n-1 {
            for j in 0..<n-i-1 {
                if arr[j] > arr[j+1] {
                    // swap
                    let temp = arr[j]
                    arr[j] = arr[j+1]
                    arr[j+1] = temp
                }
            }
        }
        
        return arr
    }
}

let bubbleSort = BubbleSort()
bubbleSort.sort([5, 4, 3, 2, 1])
```
## Merge Sort
Continuously combining two smaller sorted arrays into one larger sorted array.

Big-O-Notation is O(nlogn)

Step 1) Splitting Phase: Continuously dividing the array until it gets to its smallest parts. Takes each element of that array and divides over and over again (%2) until we essentially get an array with a single element. 

This splitting phase Big-O-Notation is O(logn)

Step 2) Combining Phase: Continuously combines the smaller unsorted arrays into larger sorted arrays.

This combining phase Big-O-Notation is O(n)
