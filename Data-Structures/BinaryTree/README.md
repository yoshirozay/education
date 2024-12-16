# Binary Trees

## Overview
A Binary Tree is a hierarchical data structure where data is stored in nodes, with each node having at most two children. This structure allows for efficient data organization and retrieval, making it fundamental in computer science.

## Performance Characteristics
* Insertion: O(log n) for balanced trees
* Search: O(log n) for balanced trees
* Deletion: O(log n) for balanced trees
* Space Complexity: O(n)
  
### Binary Tree Search

During a Binary Tree Search, the search asks the tree a simple question. Is the value I am looking for bigger or smaller than this current node? If smaller, go to the left, if bigger, go to the right. This process splits the tree in half each layer it does down. This is why the process is O(log n), because each layer splits the total time in half. This is the binary tree's killer feature, splitting the run time in half.

```swift
 func find(key: Int) -> Int? {
        guard let root = root else { return nil }
        guard let node = find(root, key) else { return nil }
        
        return node.key
    }

    private func find(_ node: Node?, _ key: Int) -> Node? {
        guard let node = node else { return nil }
        
        if node.key == key {
            return node
        } else if key < node.key {
            return find(node.left, key)
        } else if key > node.key {
            return find(node.right, key)
        }
        return nil
        // Note: duplicate keys not allowed so don't need to check
    }

```

## Inserting
Similar process to Searching, the search asks the tree a simple question. Is the value I am looking for bigger or smaller than this current node? If smaller, go to the left, if bigger, go to the right. Eventually, it will find the correct location and Insert into the Binary Search Tree

```swift
func insert(key: Int) {
        root = insertItem(root, key)
    }
    
    private func insertItem(_ node: Node?, _ key: Int) -> Node {
        
        // If node is nil - set it here. We are done.
        guard let node = node else {
            let node = Node(key)
            return node
        }
        
        if key < node.key {
            node.left = insertItem(node.left, key)
        }
        if key > node.key {
            node.right = insertItem(node.right, key)
        }
        
        // If we get here we have have hit the bottom of our tree with a duplicate.
        // Since duplicates are not allowed in BSTs, simply ignore the duplicate,
        // and return our fully constructed tree. We are done!
        return node;
    }
```

## Tree Types

### Full Binary Tree
* Every node has either 0 or 2 children
* No node has exactly one child
* Maximizes potential for balanced data distribution
* Useful for expression parsing and evaluation

### Perfect Binary Tree
* All interior nodes have exactly two children
* All leaves are at the same level
* Total number of nodes is (2^h+1) - 1, where h is height
* Rarely found in practice but serves as a theoretical ideal

### Balanced Binary Tree
* Height difference between left and right subtrees is at most 1
* Ensures O(log n) operations in most cases
* Self-balancing trees (like AVL trees) maintain this property automatically
* Most practical applications aim for balanced trees

## Traversal Methods

### Breadth-First Search (BFS)
* Explores tree level by level
* Uses a queue to track nodes to visit
* Ideal when solution is likely near the root
* Common applications:
 * Level-order traversal
 * Finding shortest path
 * Social network connections
 * Web crawling

### Depth-First Search (DFS)
* Explores tree by going as deep as possible
* Uses a stack (or recursion) to track nodes
* Three main variants:
 * Pre-order (Root, Left, Right)
 * In-order (Left, Root, Right)
 * Post-order (Left, Right, Root)
* Best when:
 * Solution is likely to be deep in the tree
 * Memory is a constraint (uses less space than BFS)
 * Need to explore all paths to leaves


## Common Applications
* File system organization
* Database indexing
* Expression evaluation
* Decision trees in artificial intelligence
* Huffman coding in data compression
* Abstract Syntax Trees in compilers

