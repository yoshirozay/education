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
