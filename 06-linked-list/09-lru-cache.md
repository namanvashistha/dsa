# LRU Cache

## 📋 Problem Statement

Design a data structure that follows the constraints of a **Least Recently Used (LRU) cache**.

Implement the `LRUCache` class:
- `LRUCache(int capacity)` Initialize the LRU cache with positive size capacity.
- `int get(int key)` Return the value of the key if it exists, otherwise return -1.
- `void put(int key, int value)` Update the value if the key exists. Otherwise, add the key-value pair. If the number of keys exceeds the capacity, evict the least recently used key.

The functions `get` and `put` must each run in `O(1)` average time complexity.

---

## 🧠 Thought Process

### Challenge
O(1) for both lookup AND maintaining order?

### Key Insight 💡
Combine:
- **HashMap:** O(1) lookup
- **Doubly Linked List:** O(1) insert/delete, maintains order

Most recent at HEAD, least recent at TAIL.

---

## 💡 Solution

```python
class Node:
    def __init__(self, key=0, val=0):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

class LRUCache:
    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {}  # key -> Node
        
        # Dummy head and tail
        self.head = Node()
        self.tail = Node()
        self.head.next = self.tail
        self.tail.prev = self.head
    
    def _remove(self, node):
        prev, next = node.prev, node.next
        prev.next = next
        next.prev = prev
    
    def _add_to_front(self, node):
        node.next = self.head.next
        node.prev = self.head
        self.head.next.prev = node
        self.head.next = node
    
    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        
        node = self.cache[key]
        self._remove(node)
        self._add_to_front(node)
        return node.val
    
    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self._remove(self.cache[key])
        
        node = Node(key, value)
        self.cache[key] = node
        self._add_to_front(node)
        
        if len(self.cache) > self.cap:
            # Remove LRU (at tail)
            lru = self.tail.prev
            self._remove(lru)
            del self.cache[lru.key]
```

---

## 📊 Visual Representation

```
Initial capacity=2:

put(1, 1): 
  head ↔ [1:1] ↔ tail

put(2, 2):
  head ↔ [2:2] ↔ [1:1] ↔ tail

get(1):
  head ↔ [1:1] ↔ [2:2] ↔ tail  (1 moved to front)

put(3, 3): (capacity exceeded)
  evict [2:2] (tail)
  head ↔ [3:3] ↔ [1:1] ↔ tail
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| get | O(1) | O(capacity) |
| put | O(1) | O(capacity) |

---

## 🎯 Key Takeaways

1. **HashMap + Doubly Linked List** - Classic combination
2. **Dummy nodes** - Simplify edge cases
3. **Move to front on access** - Update recency
4. **Evict from tail** - LRU element

---

## 🔗 Related Problems
- LFU Cache
- Design HashMap
- All O(1) Data Structure
