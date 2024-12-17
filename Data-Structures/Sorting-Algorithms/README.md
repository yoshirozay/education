# Sorting Algorithms

## Bubble Sort
Bubble Sort is an algorithm that sorts an array from least to greatest by moving the largest numbers to the end of the array. It works by:
- Starting with the first number and comparing it to the number on its right
- Moving the greater of the two numbers forward
- Repeating this comparison process through the array until the greatest number reaches the end
- Continuing until the entire array is sorted

Time Complexity: O(N²)

### Implementation in Swift
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
Merge Sort works by continuously combining two smaller sorted arrays into one larger sorted array. The algorithm consists of two main phases:

### 1. Splitting Phase (O(log n))
- Continuously divides the array until it reaches its smallest parts
- Takes each element and divides repeatedly (by 2) until reaching single-element arrays

### 2. Combining Phase (O(n))
- Combines the smaller unsorted arrays into larger sorted arrays
- Merges these arrays while maintaining sort order

Total Time Complexity: O(n log n)

### Implementation in Swift
```swift
class MergeSort {
    func sort(_ array: [Int]) -> [Int] {
        guard array.count > 1 else { return array }
        
        let middleIndex = array.count / 2
        
        let leftArray = sort(Array(array[0..<middleIndex]))
        let rightArray = sort(Array(array[middleIndex..<array.count]))
        
        return merge(leftArray, rightArray)
    }
    
    private func merge(_ leftArray: [Int], _ rightArray: [Int]) -> [Int] {
        var leftIndex = 0
        var rightIndex = 0
        var mergedArray: [Int] = []
        
        while leftIndex < leftArray.count && rightIndex < rightArray.count {
            if leftArray[leftIndex] < rightArray[rightIndex] {
                mergedArray.append(leftArray[leftIndex])
                leftIndex += 1
            } else {
                mergedArray.append(rightArray[rightIndex])
                rightIndex += 1
            }
        }
        
        // Add remaining elements
        mergedArray.append(contentsOf: leftArray[leftIndex...])
        mergedArray.append(contentsOf: rightArray[rightIndex...])
        
        return mergedArray
    }
}

let mergeSort = MergeSort()
mergeSort.sort([5, 4, 3, 2, 1])
```

## Quick Sort
Quick Sort is the fastest sorting algorithm with a time complexity of O(n log n). Here's how it works:

1. Select a pivot point in the array (ideally near the middle)
2. Partition numbers around this pivot:
   - Numbers greater than pivot and lower index move right
   - Numbers lesser than pivot and greater index move left
3. Process:
   - Set left and right pointers
   - Compare values at pointers to pivot
   - Swap values when finding a number greater than pivot on left and smaller than pivot on right
   - Continue until all numbers are properly positioned relative to pivot
4. Repeat process on resulting subarrays until fully sorted

Time Complexity: O(n log n)
```swift
// Implementation of Merge Sort algorithm

class MergeSort {
    func sort(_ array: [Int]) -> [Int] {
        // Base case: if array has 1 or fewer elements, it's already sorted
        guard array.count > 1 else { return array }
        
        // Find the middle point to divide array into two halves
        let middleIndex = array.count / 2
        
        // Split array and recursively sort both halves
        let leftArray = sort(Array(array[0..<middleIndex]))
        let rightArray = sort(Array(array[middleIndex..<array.count]))
        
        // Merge the sorted halves
        return merge(leftArray, rightArray)
    }
    
    private func merge(_ leftArray: [Int], _ rightArray: [Int]) -> [Int] {
        var leftIndex = 0
        var rightIndex = 0
        var mergedArray: [Int] = []
        
        // Compare elements from both arrays and merge in sorted order
        while leftIndex < leftArray.count && rightIndex < rightArray.count {
            if leftArray[leftIndex] < rightArray[rightIndex] {
                mergedArray.append(leftArray[leftIndex])
                leftIndex += 1
            } else {
                mergedArray.append(rightArray[rightIndex])
                rightIndex += 1
            }
        }
        
        // Add any remaining elements from the left array
        while leftIndex < leftArray.count {
            mergedArray.append(leftArray[leftIndex])
            leftIndex += 1
        }
        
        // Add any remaining elements from the right array
        while rightIndex < rightArray.count {
            mergedArray.append(rightArray[rightIndex])
            rightIndex += 1
        }
        
        return mergedArray
    }
}

// Example usage:
let mergeSort = MergeSort()
let unsortedArray = [64, 34, 25, 12, 22, 11, 90]
let sortedArray = mergeSort.sort(unsortedArray)
print("Original array: \(unsortedArray)")
print("Sorted array: \(sortedArray)")
```

### Implementation in Swift
```swift
class QuickSort {
    func sort(_ array: [Int]) -> [Int] {
        var arr = array
        quickSort(&arr, low: 0, high: arr.count - 1)
        return arr
    }
    
    private func quickSort(_ array: inout [Int], low: Int, high: Int) {
        if low < high {
            let pivotIndex = partition(&array, low: low, high: high)
            quickSort(&array, low: low, high: pivotIndex - 1)
            quickSort(&array, low: pivotIndex + 1, high: high)
        }
    }
    
    private func partition(_ array: inout [Int], low: Int, high: Int) -> Int {
        let pivot = array[high]
        var i = low - 1
        
        for j in low..<high {
            if array[j] <= pivot {
                i += 1
                array.swapAt(i, j)
            }
        }
        
        array.swapAt(i + 1, high)
        return i + 1
    }
}

let quickSort = QuickSort()
quickSort.sort([5, 4, 3, 2, 1])
```
