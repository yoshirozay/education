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
