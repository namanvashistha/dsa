# Kth Largest Element in a Stream

## 📋 Problem Statement

Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:
- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
- `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.

### Examples

```
Input: ["KthLargest", "add", "add", "add", "add", "add"]
       [[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output: [null, 4, 5, 5, 8, 8]
```

---

## 🧠 Thought Process

### Key Insight 💡
Maintain a **min heap of size k**:
- Top of heap = kth largest
- If heap size > k, remove smallest
- New element: add, then potentially remove

---

## 💡 Solution

```python
import heapq

class KthLargest:
    def __init__(self, k: int, nums: list[int]):
        self.k = k
        self.heap = []
        
        for num in nums:
            self.add(num)
    
    def add(self, val: int) -> int:
        heapq.heappush(self.heap, val)
        
        if len(self.heap) > self.k:
            heapq.heappop(self.heap)
        
        return self.heap[0]
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| Constructor | O(n log k) | O(k) |
| add | O(log k) | O(1) |

---

## 🎯 Key Takeaways

1. **Min heap of size k** - Top is kth largest
2. **Pop when > k** - Remove smallest
3. **O(log k) add** - Efficient for streaming

---

## 🔗 Related Problems
- Kth Largest Element in Array
- Find Median from Data Stream
