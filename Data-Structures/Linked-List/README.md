# Linked List Overview

## Limitations of Arrays
- Inserting at the front takes linear time O(N)
- Arrays require significant space due to doubling in size when full
- Need for a more flexible structure that allows quick front insertions and dynamic resizing

## What is a Linked List?
A Linked List is a linear collection of data elements sequentially linked together by a series of nodes (analogous to cars on a train). The structure consists of three main elements:
1. Head 
2. Node
3. Tail

## Key Features
- Elements are added at the head
- The tail always points to nil (the ether)  
- Each node acts like a train car with a pointer to the next node

## Performance Characteristics
- **Primary Advantage**: Adding elements to the front in O(1) constant time
- **Traversal**: Walking a Linked List is O(n)
 - Note: The presence of a "while" loop typically indicates list traversal

## Implementation Notes
Head → Node → Node → Tail → nil

``` swift

class Node {
    var data: Int
    var next: Node?
    
    init(_ data: Int, _ next: Node? = nil) {
        self.data = data
        self.next = next
    }
}

let node3 = Node(3)
let node2 = Node(2, node3)
let node1 = Node(1, node2)

```
### Add to Front
Updating Linked Lists is all about manipulating pointers, it's easier to think about Linked List when the node is an UUID(). To update the head of the node, you simply point the head of the Linked List to the new UUID, and update the new UUID's pointer (new head) to the previous head. This process is O(1), Constant Time

``` swift
   func addFront(_ data: Int) {
        let newNode = Node(data)
        newNode.next = head
        head = newNode
    }
```
### Insert to Position
As for Inserting a new element at a specific location, you need to replace the UUID pointer from the node before it with the new UUID, and give the new node the old UUID.

```swift
  func insert(position: Int, data: Int) {
        if position == 0 {
            addFront(data)
            return
        }
        let newNode = Node(data)
        var currentNode = head
        
        for _ in 0..<position - 1 {
            currentNode = currentNode?.next!
        }
        currentNode?.next = newNode
        newNode.next = currentNode?.next
    }
```
