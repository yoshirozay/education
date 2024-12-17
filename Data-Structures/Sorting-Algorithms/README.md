## Bubble Sort
Sorts the array from least to greatest by moving the largest numbers to the end of the array. Starts by comparing the first number to the number on the right. It takes the greater of the two numbers, and repeats the comparison process all the way down the array until the greatest number is at the end (right) of the array.

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
