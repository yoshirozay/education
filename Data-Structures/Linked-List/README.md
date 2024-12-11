Few things arrays cant do? Inserting at the front, it takes linear time O(N). Arrays can take a lot of space because they have to double in size when they are full. We need a structure that can quickly add elements at the front as well as contstantly resize.

A LinkedList is a linear collection of data elements sequentially linked together by a series of nodes (cars on a train). Three elements to a linked list: head, node, and tail. We add elements to the head, the tail always points to the ether (nil) and each node is a car on the train with a pointer, pointing to the next car on the train.

The LinkedList's killer feature is that it can add new elements to the front at O(1), Constant Time.

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
