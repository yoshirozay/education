# Stack Data Structure

## Overview
A Stack is a common data structure modeled after everyday objects where items can be added and removed from the top. It follows the Last In First Out (LIFO) principle.

## Operations
- **Push**: Adding items to the stack - O(1)
- **Pop**: Removing items from the stack - O(1)

## Key Features
- Last In First Out (LIFO) structure
- Both push and pop operations occur in constant time O(1)
- Simple and intuitive implementation

## Common Applications
- Undo/Redo functionality in applications
- Browser back/forward navigation
- Function call management in programming languages

## Performance Characteristics
- **Primary Advantage**: O(1) constant time for both push and pop operations
- Ideal for scenarios requiring LIFO data management

```swift
class Stack<T> {
    private var array: [T] = []
    
    func push(_ item: T) {
        array.append(item)
    }
    
    func pop() -> T? {
        array.popLast()
    }
    
    func peek() -> T? {
        array.last
    }
    
    var isEmpty: Bool {
        array.isEmpty
    }
    
    var count: Int {
        array.count
    }
}
```

# Queue Data Structure

## Overview
A Queue is a data structure that follows the First In First Out (FIFO) principle, operating inversely to Linked Lists in terms of performance characteristics.

## Performance Characteristics
- **Adding to Back**: O(1) constant time (efficient)
- **Adding to Front**: O(N) linear time (requires traversal)
- Operations follow FIFO order

## Key Features
- First In First Out (FIFO) structure
- Optimized for back-end operations
- Requires full traversal for front-end modifications

## Implementation Notes
- Excellent for situations requiring FIFO processing
- Performance trade-off: Fast rear operations, slower front operations
- Contrast with Linked List: Queues excel at back operations while Linked Lists excel at front operations

## Common Applications
- Task scheduling
- Resource management
- Print job processing
- Message buffering

```swift
/*
 First-in first-out (FIFO)
 enqueue O(1) dequeue O(n)
 */

class Queue<T> {
    private var array: [T] = []
    
    func enqueue(_ item: T) {
        array.append(item)
    }
    
    func dequeue() -> T? {
        if isEmpty {
            return nil
        } else {
            return array.removeFirst()
        }
    }
    
    var isEmpty: Bool {
        return array.isEmpty
    }
    
    var count: Int {
        return array.count
    }
    
    func peek() -> T? {
        return array.first
    }
}
```

Stacks & Queues are often built using Arrays or Linked Lists, but mainly the Array because the Swift Array has push and pop like functionality already built in.

## Interview Question
 ### #1
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
```swift
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
 ### #2
/*
 Rotate array to left N times.
 
 For example, given

     A = [3, 8, 9, 7, 6]
     K = 3
 the function should return [9, 7, 6, 3, 8]. Three rotations were made:

     [3, 8, 9, 7, 6] -> [8, 9, 7, 6, 3]
     [8, 9, 7, 6, 3] -> [9, 7, 6, 3, 8]
     [9, 7, 6, 3, 8] -> [7, 6, 3, 8, 9]
     
 */

 ```swift
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
 ### #3
  Giving a String, write a function that reverses the String using a stack.
  ```swift
func solution(_ text: String) -> String {
    // Do your work here...
    var chars = Array(text)
    var results = [Character]()
    var count = chars.count-1
    while count >= 0 {
        let last = chars[count]
        results.append(last)
        count = count - 1
    }
    print("results = \(results)")
    return String(results)
}

solution("abc") // cba
solution("Would you like to play a game?")

```
### #4
Balanced brackets
 https://www.hackerrank.com/challenges/balanced-brackets/problem
 
 A bracket is considered to be any one of the following characters: (, ), {, }, [, or ].

 Two brackets are considered to be a matched pair if the an opening bracket (i.e., (, [, or {) occurs to the left of a closing bracket (i.e., ), ], or }) of the exact same type. There are three types of matched pairs of brackets: [], {}, and ().

 A matching pair of brackets is not balanced if the set of brackets it encloses are not matched. For example, {[(])} is not balanced because the contents in between { and } are not balanced. The pair of square brackets encloses a single, unbalanced opening bracket, (, and the pair of parentheses encloses a single, unbalanced closing square bracket, ].

 By this logic, we say a sequence of brackets is balanced if the following conditions are met:

 It contains no unmatched brackets.
 The subset of brackets enclosed within the confines of a matched pair of brackets is also a matched pair of brackets.
 Given  strings of brackets, determine whether each sequence of brackets is balanced. If a string is balanced, return YES. Otherwise, return NO.

 
func isBalanced(s: String) -> String {

    var st = [Character]()
    
    for c in s {
        switch c {
        case "{", "(", "[":
            st.append(c)
        case "}":
            if (st.isEmpty || (st.last != "{")) {
                return "NO"
            }
            st.popLast()
        case ")":
            if (st.isEmpty || (st.last != "(")) {
                return "NO";
            }
            st.popLast()
        case "]":
            if (st.isEmpty || (st.last != "[")) {
                return "NO";
            }
            st.popLast()
        default:
            print("breaking \(c)")
        }
    }
    
    return st.isEmpty ? "YES" : "NO"
}

isBalanced(s: "{[()]}") // Yes

isBalanced(s: "[()]}") // No

isBalanced(s: "{}()(){}((){})({[[({({(){}{}}){}})]{({()}((())))}()]})(({}(()){[][]}){()}(({}{}))())()[](){{((){})}}()([[]])[][]()({}((([()]{})())[][[()]]())){{}}[]{()}()[][]{}([])[]{({})}{}{{}{[[]]}[]{}}{[()]}[]{(([{{[{[]}]}[{}]}]))}(){}{{}}[]((([])([{(){}[(()[]((()(){})({([]({{{[]{}}[({})()({}{([()])()()[]{}})][{[]}]{{}([]({{{(()(({}[[[{{}}]]{{[()]([[{{}([[]][([{{}}(([])[][({()}())()({}[])]{}[])]())[]]){}}[]]])([]({{[[][]{[]}[]]}}{}(){[]}))}()[]((){{}()[{[[()]]}()]}[()]{})}][]{}))())}(())}{{[]}{}}({[([{[{[[[]]]{()}[]}]{}}()((({{{{({{(){}}}[[()]()[]]())({{{[]}{{[[{{[{}]}}[][]]]([][](()(()[]){{}}))([])}}}}[{}{}])[(){{()()}{(())}()}]{(){{}[]{}[][{[]([[]()]{(){[{}[()]][{}{}]{(){}}}{[]}}{[]}[]){[]}[]}][((){}{}[[[[{{}()[([({{[[][{{()}(([[]][[[[[[[{}]][{}]]]()](())[()[][]({({[][][[]{}][]}{})}{({})([[][]({}{[]})])[([([])][[]{([])(({}))}](()[]){[[]]}({}))]}[])()]]]))([{}()()([([[{}][()]][])])][[[{}][][]({[]})][(({{()}}))]])}]]}})])]}]]]])]}}}}}})))])]})}))}}}))})))]}])))") 
// Yes
