Few things arrays cant do? Inserting at the front, it takes linear time O(N). Arrays can take a lot of space because they have to double in size when they are full. We need a structure that can quickly add elements at the front as well as contstantly resize.

A LinkedList is a linear collection of data elements sequentially linked together by a series of nodes (cars on a train). Three elements to a linked list: head, node, and tail. We add elements to the head, the tail always points to the ether (nil) and each node is a car on the train with a pointer, pointing to the next car on the train.

The LinkedList's killer feature is that it can add new elements to the front at O(1), Constant Time.

Walking a Linked List is O(n), whenever we see a "while" loop, we are walking the linked list

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

Updating Linked Lists is all about manipulating pointers, it's easier to think about Linked List when the node is an UUID(). To update the head of the node, you simply point the head of the Linked List to the new UUID, and update the new UUID's pointer (new head) to the previous head. This process is O(1), Constant Time

``` swift
   func addFront(_ data: Int) {
        let newNode = Node(data)
        newNode.next = head
        head = newNode
    }
```
As for Inserting a new element at a specific location, you need to replace the UUID pointer from the node before it with the new UUID, and give the new node the old UUID.
