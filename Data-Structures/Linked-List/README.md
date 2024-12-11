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
        newNode.next = currentNode?.next
        currentNode?.next = newNode
    }
```
### Deleting
Similar to inserting at position, to delete a node you simply need to remove the UUID reference of the deletion target from the node prior and reassign it to the node infront of the deletion target. If the deletion target is the head of the linked list, you simply reasign the head to the second node. This process is O(n) since you need to walk through the list to get to the deletion location.

```swift
    func delete(at position: Int) {
        if position == 0 {
            self.deleteFirst()
            return
        }
        var node = head
        var previousNode: Node?
        for _ in 0..<position {
            previousNode = node
            node = node?.next
        }
        previousNode?.next = node?.next
    }
```
### Clearing a Linked List
By simply setting the head of the list = nil, the rest of the list is no longer referenced so Swift will clean up the rest of the list 

## Interview Question 
Find Merge Point of Two Lists

 Given pointers to the head nodes of 2 linked lists that merge together at some point, find the node where the two lists merge. The merge point is where both lists point to the same node, i.e. they reference the same memory location. It is guaranteed that the two head nodes will be different, and neither will be NULL. If the lists share a common node, return that node's data value.

 Note: After the merge point, both lists will share the same node pointers.

 ```swift
func findMerge(headA: Node?, headB: Node?) -> Int? {
    if headA == nil { return nil }
    
    var result = [Int]()
    var node = headA
    result.append(node!.data)
    
    while node?.next != nil {
        result.append(node!.next!.data)
        node = node?.next
    }
    print(result)
    var nodeB = headB
    while nodeB?.next != nil {
        if result.contains(nodeB!.data) {
            return nodeB?.data
        }
        nodeB = nodeB?.next
    }
    if result.contains(nodeB!.data) {
        return nodeB?.data
    }
    return nil
}
```

 Detect A Cycle
 https://www.hackerrank.com/challenges/ctci-linked-list-cycle/problem
 https://en.wikipedia.org/wiki/Cycle_detection#Floyd's_Tortoise_and_Hare
 
 A linked list is said to contain a cycle if any node is visited more than once while traversing the list. For example, in the following graph there is a cycle formed when node 5 points back to node 3.
 
        4
      /   \
 1 2 3      5
     \_____/

```swift
class Node {
    var data: Int
    weak var next: Node?
    
    init(_ data: Int, _ next: Node? = nil) {
        self.data = data
        self.next = next
    }
}

func hasCycle(first: Node) -> Bool {
    var node = first
    var previousNodes = [Node]()
    while node.next != nil {
        previousNodes.append(node)
        node = node.next!
            if let firstIndex = previousNodes.firstIndex(where: {$0.data == node.data}) {
                return true
        }
    }
    // here...
    return false
}

let node5 = Node(5)
let node4 = Node(4)
let node3 = Node(3)
let node2 = Node(2)
let head = Node(1)

head.next = node2
node2.next = node3
node3.next = node4
node4.next = node5
node5.next = node3

hasCycle(first: head)
```
