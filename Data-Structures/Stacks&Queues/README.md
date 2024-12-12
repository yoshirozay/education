Stacks are every day objects where you can add and remove things from the stack, this action of putting items on and off (pushing and popping) are O(1) operations. Last In First Out (LIFO). This is great for undo / redo functions, back and forward in the browser. 

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

Queue's have the inverse Big O Notation as Linked Lists, they can append to the back of the queue lightning fast O(1) but are slower to add to the front of the queue O(N). First in First Out (FIFO)

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
