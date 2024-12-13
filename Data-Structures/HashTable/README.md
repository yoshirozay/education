# Hash Tables in Swift (Dictionaries)

## Overview
A Hash Table is a data structure that implements key-value pair lookups with exceptional performance characteristics. In Swift, this is implemented as a Dictionary.

## Hash Functions
- Takes any object as input
- Calculates a nearly unique numerical representation
- Used for generating keys for later lookup
- Produces deterministic results (same input always yields same output)

## Core Operations - O(1)
- Search
- Insert
- Delete

## Key Concepts

### Hash to Index Conversion
1. Hash function generates a large number
2. Large number is modulated (%) by array size
3. Result becomes the index for storage/lookup

## Collision Handling
* **What is a Collision?**
  * Occurs when two different items generate the same index
  * Can happen even with excellent hash functions
* **Resolution Method**
  * Uses chaining via Linked List
  * Multiple values can be stored at same index
  * Maintains O(1) average case performance

## Best Practices
* Choose appropriate initial size to minimize resizing
* Implement good hash functions that distribute values evenly
* Monitor load factor to maintain performance
* Consider collision frequency in hash function design

## Common Applications
* Caching
* Database indexing
* Symbol tables
* Unique value tracking

```swift
// Strings, Integers, Floating point numbers and Booleans
// are all hashable by default.
let stringsAreHashable = "abc".hashValue

struct GridPoint {
    var x: Int
    var y: Int
    
    var hashValue: Int {
        // XOR properties together seeded with a prime number
        return x.hashValue ^ y.hashValue &* 16777619
    }
}

let mainBase = GridPoint(x: 131, y: 541)
let hashCode = mainBase.hashValue

// Modulus operator
let even = 2 % 2
let odd = 3 % 2 // remainder 1

let initialSize = 16
let index = hashCode % initialSize // guaranteed fit

let indexPositive = abs(index)


// Linked List
class HashEntry {
    var key: String
    var value: String
    var next: HashEntry?
    
    init(_ key: String, _ value: String) {
        self.key = key
        self.value = value
    }
}

class HashTable {
    private static let initialSize = 256
    private var entries = Array<HashEntry?>(repeating: nil, count: initialSize)
    
    func put(_ key: String, _ value: String) {
        // Get the index
        let index = getIndex(key)
        
        // Create entry
        let entry = HashEntry(key, value)
        
        // If entry is not already there - store it
        if entries[index] == nil {
            entries[index] = entry
        }
        // else handle collision by appending to our linked list
        else {
            var collisions = entries[index]
            
            // Walk to the end
            while collisions?.next != nil {
                collisions = collisions?.next
            }
            
            // Add collision there
            collisions?.next = entry
        }
    }
    
    func get(_ key: String) -> String? {
        // Get the index
        let index = getIndex(key)
        
        // Get current list of entries for this index
        let possibleCollisions = entries[index]
        
        // Walk our linked list looking for a possible match on the key (that will be unique)
        var currentEntry = possibleCollisions
        while currentEntry != nil {
            if currentEntry?.key == key {
                return currentEntry?.value
            }
            currentEntry = currentEntry?.next
        }
        
        return nil
    }
    
    private func getIndex(_ key: String) -> Int {
        // Get the key's hash code
        let hashCode = abs(key.hashValue)
        
        // Normalize it into an acceptable index
        let index = hashCode % HashTable.initialSize
        print("\(key) \(hashCode) \(index)")
        
        // Forced collision for demonstration purposes
        if key == "John Smith" || key == "Sandra Dee" {
            return 152
        }
        
        return index
    }

    func prettyPrint() {
        for entry in entries {
            if entry == nil {
                continue
            }
            if entry?.next == nil {
                // nothing else there
                print("key: \(String(describing: entry?.key)) value: \(String(describing: entry?.value))")
            } else {
                // collisions
                var currentEntry = entry
                while currentEntry?.next != nil {
                    print("💥 key: \(String(describing: currentEntry?.key)) value: \(String(describing: currentEntry?.value))")
                    currentEntry = currentEntry?.next
                }
                print("💥 key: \(String(describing: currentEntry?.key)) value: \(String(describing: currentEntry?.value))")
            }
        }
    }
    
    subscript(key: String) -> String? {
        get {
            get(key)
        }
        set(newValue) {
            guard let value = newValue else { return }
            put(key, value)
        }
    }
}

let hashTable = HashTable()
hashTable.put("John Smith", "521-1234")
hashTable.put("Lisa Smith", "521-8976")
hashTable.put("Sam Doe", "521-5030")
hashTable.put("Sandra Dee", "521-9655")
hashTable.put("Ted Baker", "418-4165")

hashTable.prettyPrint()

hashTable.get("John Smith")
hashTable.get("Lisa Smith")
hashTable.get("Sam Doe")
hashTable.get("Sandra Dee")
hashTable.get("Ted Baker")
hashTable.get("Tim Lee")

hashTable["Kevin Flynn"] = "The grid"
hashTable["Kevin Flynn"]

```
