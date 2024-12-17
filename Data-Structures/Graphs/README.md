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

## Interview Question

 ```swift
/*
 You are given in undirected graph consisting of N vertices, numbered from 1 to N, and M edges.
 
 The graph is described by two arrays, A and B, both of length M. A pair A[K] and B[K] for K from 0 to M-1, describe the edge between vertex A[K] and vertex B[K].
 
 Your task is to check whether the given graph contains a path from vertex 1 to vertex N going through all the vertices, one-by-one, in increasing order of the numbers. All connections on the path should be direct.
 
 Write a function, that given an integer N and two arrays A and B of M integers each, returns true if there exists a path from vertex 1 to N going through all vertices, one-by-one, in increasing order, or false other wise.
 
 Example 1:

          ┌─────┐
   ┌──────│  3  │──────┐
   │      └─────┘      │
   │         │         │
┌─────┐      │      ┌─────┐
│  2  │      │      │  4  │
└─────       │      └─────┘
   │      ┌─────┐      │
   └──────│  1  │──────┘
          └─────┘
 
 Given N = 4
       A = [1, 2, 4, 4, 3]
       B = [2, 3, 1, 3, 1]
       Function should return true.
 
 There is a path (1 > 2 > 3 > 4) using edges (1, 2), (2, 3), (4, 3).
 
 Example 2:

          ┌─────┐
   ┌──────│  4  │──────┐
   │      └─────┘      │
   │         │         │
┌─────┐      │      ┌─────┐
│  2  │      │      │  3  │
└─────       │      └─────┘
   │      ┌─────┐      │
   └──────│  1  │──────┘
          └─────┘
 
 Given N = 4
       A = [1, 2, 1, 3]
       B = [2, 4, 3, 4]
       Function should return false.
 
 There is no path (1 > 2 > 3 > 4) as there is no direct connection from vertex 2 to vertex 3.
 
 Example 3:

 ┌─────┐
 │  1  │
 └─────┘
                             
┌─────┐    ┌─────┐    ┌─────┐   ┌─────┐    ┌─────┐
│  2  │────┤  3  │────│  4  │───│  5  │────│  6  │
└─────┘    └─────┘    └─────┘   └─────┘    └─────┘
 
 Given N = 6
       A = [2, 4, 5, 3]
       B = [3, 5, 6, 4]
       Function should return false.
  
 Example 4:

 ┌─────┐    ┌─────┐    ┌─────┐
 │  1  │────┤  2  │────│  3  │
 └─────┘    └─────┘    └─────┘

 Given N = 3
       A = [1, 3]
       B = [2, 2]
       Function should return true.

 
 Example 5:

 ┌─────┐    ┌─────┐    ┌─────┐
 │  2  │────┤  3  │────│  4  │
 └─────┘    └─────┘    └─────┘
 
 Given N = 3
       A = [2, 3]
       B = [3, 4]
       Function should return false.

 */


struct Edge: Equatable {
    let from: Int
    let to: Int
    
    init(_ from: Int, _ to: Int) {
        self.from = from
        self.to = to
    }
}

func solution(_ A: [Int], _ B: [Int]) -> Bool {
    guard A.count > 0 && B.count > 0 else { return false }
    let maxValue = max(A.max()!, B.max()!)
    
    // make edges
    var edges: [Edge] = []
    for n in 0..<A.count {
        edges.append(Edge(A[n], B[n]))
    }

    // walk cases
    if A.count == 1 {
        return edges.contains(Edge(1, 2)) || edges.contains(Edge(2, 1))
    } else if A.count == 2 {
        return (edges.contains(Edge(1, 2)) || edges.contains(Edge(2, 1))) &&
               (edges.contains(Edge(2, 3)) || edges.contains(Edge(3, 2)))
    }
    
    for i in 1..<maxValue - 1 {
        if edges.contains(Edge(i, i+1)) || edges.contains(Edge(i+1, i)) { continue }
        else { return false }
    }

    return true
}

// Tips
// 1. Work out on paper
// 2. Work on simple case manually.
// 3. Read problem carefully.

//var edges: [Edge] = []
//edges.insert(Edge(1, 2))
//edges.insert(Edge(3, 2))
//
// walk in order
//edges.contains(Edge(1, 2)) || given.contains(Edge(2, 1))
//edges.contains(Edge(2, 3)) || given.contains(Edge(3, 2))



/*
 Example 1:

          ┌─────┐
   ┌──────│  3  │──────┐
   │      └─────┘      │
   │         │         │
┌─────┐      │      ┌─────┐
│  2  │      │      │  4  │
└─────       │      └─────┘
   │      ┌─────┐      │
   └──────│  1  │──────┘
          └─────┘
 
 Given N = 4
       A = [1, 2, 4, 4, 3]
       B = [2, 3, 1, 3, 1]
       Function should return true.

 */
solution([1, 2, 4, 4, 3], [2, 3, 1, 3, 1]) // true

/*
 Example 2:

          ┌─────┐
   ┌──────│  4  │──────┐
   │      └─────┘      │
   │         │         │
┌─────┐      │      ┌─────┐
│  2  │      │      │  3  │
└─────       │      └─────┘
   │      ┌─────┐      │
   └──────│  1  │──────┘
          └─────┘
 
 Given N = 4
       A = [1, 2, 1, 3]
       B = [2, 4, 3, 4]
       Function should return false.
 */
solution([1, 2, 1, 3], [2, 4, 3, 4]) // false

/*
 Example 3:

 ┌─────┐
 │  1  │
 └─────┘
                             
┌─────┐    ┌─────┐    ┌─────┐   ┌─────┐    ┌─────┐
│  2  │────┤  3  │────│  4  │───│  5  │────│  6  │
└─────┘    └─────┘    └─────┘   └─────┘    └─────┘
 
 Given N = 6
       A = [2, 4, 5, 3]
       B = [3, 5, 6, 4]
       Function should return false.
 */
solution([2, 4, 5, 3], [3, 5, 6, 4]) // false

/*
 Example 4:

 ┌─────┐    ┌─────┐    ┌─────┐
 │  1  │────┤  2  │────│  3  │
 └─────┘    └─────┘    └─────┘

 Given N = 3
       A = [1, 3]
       B = [2, 2]
       Function should return true.

 */
solution([1, 3], [2, 2]) // true

/*
 
 Example 5:

 ┌─────┐    ┌─────┐    ┌─────┐
 │  2  │────┤  3  │────│  4  │
 └─────┘    └─────┘    └─────┘
 
 Given N = 3
       A = [2, 3]
       B = [3, 4]
       Function should return false.

 */

solution([2, 3], [3, 4]) // false


```
