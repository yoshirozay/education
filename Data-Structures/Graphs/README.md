# Graph Theory

## Binary Tree as a Graph
A Binary Tree is a graph, a type of graph. What are its limitations? Each node can only have two children, as well as the tree only goes from top to bottom.

## Basic Graph Definition
A Graph 'G' is an ordered pair of a set of vertices (V) and a set of edges (E). G = (V,E).

Can take any data structure and represent the nodes as Vertices, and the connections as Edges.

## Edge Types
Edges have two types, directed and undirected. Binary Tree has directed edges because they always point one direction. Undirected can go both directions (bi-lateral) meaning up and down, OR, they can simply point to any node they want.

## Weighted Graphs
Weighted Graphs, use weights to represent the estimated cost of moving from along one edge from one verticy to another. For example, if we want to find the cheapest flight or shortest distance from New York to Sydney, we can build a graph with edges and find out what the shortest path is.

## Summary
A graph is a series of Vertices and Edges that represent some problem or domain that we want to search or traverse.

## Graph Data Structures
The goal is to take each verticy and edge and somehow represent those as a simple data structure. Three very common graph data structures are

1) Edge Lists
2) Adjacency Matrices
3) Adjacency Lists

### Edge List
Take every edge in the graph, represent them as two elements in an array.
[0,1],[1,2],[0,4],[4,3],[3,1],[3,2]

Pros: Very Simple
Cons: O(n) linear search

### Adjacency Matrix
Take every edge in the graph and represent it as a 1 in a 2x2 matrix (Linear Algebra)

Pros: Constant Time O(1)
Cons: Not space efficient

### Adjacency List
Take each verticy, write down its neighbours as a list in an array. By maintaining an array of arrays or a linked list holding these array elements we can quickly build up a collection of neighbours for each verticy and look them up very quickly.

0 -> [1,4]

1 -> [2]

2 -> [ ]

3 -> [1,2]

4 -> [3]

Pros: Fast lookup, easy to find neighbours

## Breadth First Search
Start in the middle, expand our search outwards. Only after we have explored every node on the closest layer do we move to the next layer. Think of this as finding your nearest neighbour.

Keep track of each nodes we visited in a Queue (First in First Out) as we traverse through the graph. When the node is popped out of the Queue, we check to see which neighbours the node has, and add those neighbours into the Queue. Following this process will ensure we visit the higher level nodes first before visiting the lower level layers.

### Implementation in Swift

```swift
// Node class to represent vertices in the graph
class Node {
    let value: Int
    var neighbors: [Node]
    var visited: Bool
    
    init(value: Int) {
        self.value = value
        self.neighbors = []
        self.visited = false
    }
    
    func addNeighbor(_ node: Node) {
        neighbors.append(node)
    }
}

// BFS implementation
func breadthFirstSearch(startNode: Node) {
    // Create a queue and add the start node
    var queue: [Node] = []
    queue.append(startNode)
    startNode.visited = true
    
    // Process nodes in the queue
    while !queue.isEmpty {
        // Remove first node from queue
        let currentNode = queue.removeFirst()
        print("Visited node: \(currentNode.value)")
        
        // Add all unvisited neighbors to queue
        for neighbor in currentNode.neighbors {
            if !neighbor.visited {
                queue.append(neighbor)
                neighbor.visited = true
            }
        }
    }
}

// Example usage:
// Create test graph
let node1 = Node(value: 1)
let node2 = Node(value: 2)
let node3 = Node(value: 3)
let node4 = Node(value: 4)
let node5 = Node(value: 5)

// Set up connections
node1.addNeighbor(node2)
node1.addNeighbor(node3)
node2.addNeighbor(node4)
node3.addNeighbor(node4)
node3.addNeighbor(node5)

// Perform BFS starting from node1
breadthFirstSearch(startNode: node1)
// Output:
// Visited node: 1
// Visited node: 2
// Visited node: 3
// Visited node: 4
// Visited node: 5
```

## Time Complexity
- Time Complexity: O(V + E)
  - V = number of vertices
  - E = number of edges
- Space Complexity: O(V)
  - Needs to store vertices in the queue

## Key Points
1. Uses Queue (FIFO) data structure
2. Visits all neighbors at current depth before moving deeper
3. Marks nodes as visited to avoid cycles
4. Ideal for finding shortest paths
5. Explores graph in a level-by-level manner

## Depth First Search
Starts at a node, and drives deep into the graph ignoring all other nodes on the closest layer, until it hits the end of that tree. This is useful for path finding and cycle detection.

These algorithms are similar, one is based off a Queue and the other a Stack
