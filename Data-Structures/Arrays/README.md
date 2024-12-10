# Array Operations & Performance

An array is a collection of elements of the same type that can be set and retrieved by a continuous set of integers, also known as indices (or index).

## Key Characteristics

* Arrays can contain anything
* Arrays are of a fixed size (except for Swift)
* Arrays have random access O(1) - unlike linked lists, stacks, queues, or binary search trees

The ability to get/set an element at any location at O(1) "Constant Time" is what makes arrays so great. No matter how big the array is, you can reach in and get the index at Constant Time. This is what makes Array the most popular data structure.

## Core Operations

### Insert - O(n)
When we insert an element into an array, we are really doing three things:
1. Copying elements to make space
2. Inserting the new element
3. Incrementing array size

This process is O(n) Linear Time, because we are dependent on the number of elements in the array when copying.

### Delete - O(n)
Deleting an element from an array is similar to inserting, but we are copying down. It has Linear Time O(n).

### Update - O(1)
Direct access and modification of elements at any index.

## Handling Growth

What happens when the Array isn't big enough since it's a fixed size? (not in Swift)
The solution would be to:
1. Double the size of the array
2. Copy existing elements
3. Insert new element at the end

This growth process takes O(n) time.

### Swift Arrays
In Swift, every array reserves a specific amount of memory to hold its elements. This copying process only happens when you add elements to an array and that array begins to exceed its reserved capacity. Swift arrays handle the heavy lifting for us!

## Interview Questions 

 Rotate array to right N times.
 https://app.codility.com/programmers/lessons/2-arrays/cyclic_rotation/
 
 For example, given

     A = [3, 8, 9, 7, 6]
     K = 3
 the function should return [9, 7, 6, 3, 8]. Three rotations were made:

     [3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
     [6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
     [7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]

``` swift
import SwiftUI

func solution(A: [Int], K: Int) -> [Int] {
    guard !A.isEmpty else { return [] }
    guard K > 0 else { return A }
    // for each K, pop the last element and append to the beginning of array
    var array = A
    let index = array.count
    for _ in 1...K {
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

 We are given a string S representing a phone number, which we would like to reformat. String S consists of N characters: digits, spaces, and/or dashes. It contains at least two digits.
 
 Spaces and dashes in string S can be ignored. We want to reformat the given phone number is such a way that the digits are grouped in blocks of length three, separated by single dashes. If necessary, the final block or the last two blocks can be of length two.
 
 For example:
 
 S = "00-44   48 5555 8361" should become
     "004-448-555-583-61"
 
 Assume:
 - S consists only of digits (0-9), spaces, and/or dashses (-)
 - S containts at least two digits
 
 Translate:
 
 Would like to reformat a phone number string so that:
 - every third char is a "-"
 - spaces and dashes don't matter
 - if the block ends in anything other than -xxx or -xx reformat to a block of two like xx-xx (not obvious)
 
``` swift
import SwiftUI

func solution(_ S : String) -> String {
    // do your work here
    let noSpace = S.replacingOccurrences(of: " ", with: "")
    let noSpaceNoDash = noSpace.replacingOccurrences(of: "-", with: "")
    
    var count = 0
    var word = ""
    for character in noSpaceNoDash {
        count = count + 1
        word.append(character)
        if count % 3 == 0 {
            word.append("-")
        }
    }
    if word.last == "-" {
        word = String(word.dropLast())
    }
    // if second last character has a dash (-x)
    // reformat last three chars to (-xx)
    var chars = Array(word)
    let secondLastCharacter = chars[chars.count-2]
    if secondLastCharacter == "-" {
        chars.remove(at: chars.count-2)
        chars.insert("-", at: chars.count-2)
        return String(chars)
    }
    return word
}

solution("123456789")           // 123-456-789
solution("555372654")           // 555-372-654
solution("0 - 22 1985--324")    // 022-198-53-24
//
//// Edge cases
solution("01")                          // 01
solution("012")                         // 012
solution("0123")                        // 01-23
solution("0123       444")              // 012-34-44
solution("------0123       444")        // 012-34-44
