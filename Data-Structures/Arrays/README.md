What happens when an array gets too big? What happens when you an insert an element in the middle of an array?

An array is a collection of elements of the same type that can be set and retrieved by a continuous set of integers, also known as indeces (or index). 

Three things to know:

Arrays can contain anything
Arrays are of a fixed size (except for Swift)
Arrays have random access O(1), linked lists cant do this, stacks & queues can't, binary search trees can't either.

The ability to get/set an element at any location at O(1) "Constant Time" is what makes arrays so great. No matter how big the array is, you can reach in and get the index at Constant Time. This is what makes Array the most popular data structure.

Mechanics worth understanding: Insert, Delete, Update

When we insert an element into an array, we are really doing three things, we're copying, inserting, and incrementing. This process is O(n) Linear Time, because we are dependent on the number of elements in the array when copying. 

Deleting an element into an array is similar to inserting, but we are copying down. It has Linear Time O(n)

What happens when the Array isn't big enough since it's a fixed size? (not in Swift). The solution would be to double the size of the array, copy, insert a new element at the end. This process takes O(n) time. 

In Swift, every array reserves a specific amount of memory to hold its elements. This copying process only happens when you add elements to an array and that array begins to exceed its reserved capacity. Swift arrays handle the heavy lifting for us!

``` swift
import UIKit

/*
 Rotate array to right N times.
 https://app.codility.com/programmers/lessons/2-arrays/cyclic_rotation/
 
 For example, given

     A = [3, 8, 9, 7, 6]
     K = 3
 the function should return [9, 7, 6, 3, 8]. Three rotations were made:

     [3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
     [6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
     [7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]

 */

func solution(A: [Int], K: Int) -> [Int] {
    // for each K, pop the last element and append to the beginning of array
    var array = A
    for _ in 1...K {
        let index = array.count
        let lastElement = array[index-1]
        array.popLast()
        array.insert(lastElement, at: 0)
    }
    return array
}

solution(A: [1, 2, 3, 4, 5], K: 1) // 5 1 2 3 4
solution(A: [1, 2, 3, 4, 5], K: 2) // 4 5 1 2 3
solution(A: [1, 2, 3, 4, 5], K: 3) // 3 4 5 1 2

solution(A: [3, 8, 9, 7, 6], K: 3) // [9, 7, 6, 3, 8]

```
