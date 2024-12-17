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
 // BFS traversal from a given source s
    func BFS(s: Int) -> [Int] {
        
        var result = [Int]()
        
        // Mark all vertices as not visited
        var visited = adj.map { _ in false }
        
        // Create BFS Queue
        var queue = Queue<Int>()
        
        // Mark first vertex as visited and enqueue
        visited[s] = true
        print("Starting at \(s)")
        queue.add(s)
        result.append(s)
        
        while queue.count > 0 {
            let current = queue.remove()!
            print("De-queueing \(current)")
            
            // Get all the adjacent vertices of the current vertex
            // If adjacent has not being visited, mark visited and enqueue
            
            for n in adj[current] {
                if visited[n] == false {
                    visited[n] = true
                    print("Queuing \(n)")
                    queue.add(n)
                    result.append(n)
                }
            }
         }
        
        return result
    }
//
Starting at 0
De-queueing 0
Queuing 1
De-queueing 1
Queuing 4
Queuing 5
De-queueing 4
Queuing 6
De-queueing 5
Queuing 3
Queuing 2
De-queueing 6
De-queueing 3
De-queueing 2
Queuing 7
De-queueing 7
//
```

### Time Complexity
- Time Complexity: O(V + E)
  - V = number of vertices
  - E = number of edges
- Space Complexity: O(V)
  - Needs to store vertices in the queue

### Key Points
1. Uses Queue (FIFO) data structure
2. Visits all neighbors at current depth before moving deeper
3. Marks nodes as visited to avoid cycles
4. Ideal for finding shortest paths
5. Explores graph in a level-by-level manner

## Depth First Search
Starts at a node, and drives deep into the graph ignoring all other nodes on the closest layer, until it hits the end of that tree. This is useful for path finding and cycle detection.

These algorithms are similar, one is based off a Queue and the other a Stack

DPS uses a Stack instead of a Queue. Visit nodes, mark them as visited, as we visit them, we push them and pop them off the stack. In depth first, we start with our neighbours, add them to the stack (instead of the queue) and mark them as visited. We take our most recent popped value, check if it has neighbours, add the neighbors to the stack, mark the neighbour as visited, add its neighbours to the stack, pop them off, and so on. 

```swift
    func DFS(s: Int) -> [Int] {
        
        var result = [Int]()
        
        // Mark all vertices as not visited
        var visited = adj.map { _ in false }
        
        // Create DFS Stack
        var stack = Stack<Int>()
        
        // Mark first vertex as visited and enqueue
//        print("Starting at \(s)")
        visited[s] = true
        stack.push(s)
        
        while stack.count > 0 {
            let current = stack.pop()!
//            print("Popping \(current)")
            result.append(current)
            
            // Iterate over all neighbours adding to queue and popping deep as we go
            for n in adj[current] {
                if visited[n] == false {
                    visited[n] = true
//                    print("Pushing - \(n)")
                    stack.push(n)
                }
            }
        }
        
        return result
    }
//
Starting at 0
Popping 0
Pushing - 1
Popping 1
Pushing - 4
Pushing - 5
Popping 5
Pushing - 3
Pushing - 2
Popping 2
Pushing - 7
Popping 7
Popping 3
Popping 4
Pushing - 6
Popping 6
[0, 1, 5, 2, 7, 3, 4, 6]
//
```