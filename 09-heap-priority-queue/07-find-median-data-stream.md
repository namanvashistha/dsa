# Find Median from Data Stream

## 📋 Problem Statement

The median is the middle value in an ordered list. If the list size is even, the median is the mean of the two middle values.

Implement the MedianFinder class:
- `MedianFinder()` initializes the MedianFinder object.
- `void addNum(int num)` adds the integer num to the data structure.
- `double findMedian()` returns the median of all elements so far.

### Examples

```
Input: ["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
       [[], [1], [2], [], [3], []]
Output: [null, null, null, 1.5, null, 2.0]
```

---

## 🧠 Thought Process

### Key Insight 💡
Use **Two Heaps**:
- **Max Heap:** Stores smaller half
- **Min Heap:** Stores larger half

Median is at the top of heaps!

---

## 💡 Solution

```python
import heapq

class MedianFinder:
    def __init__(self):
        self.small = []  # Max heap (negate values)
        self.large = []  # Min heap
    
    def addNum(self, num: int) -> None:
        # Add to max heap (small)
        heapq.heappush(self.small, -num)
        
        # Balance: ensure small's max <= large's min
        if self.small and self.large and -self.small[0] > self.large[0]:
            val = -heapq.heappop(self.small)
            heapq.heappush(self.large, val)
        
        # Balance sizes (small can have at most 1 more)
        if len(self.small) > len(self.large) + 1:
            val = -heapq.heappop(self.small)
            heapq.heappush(self.large, val)
        if len(self.large) > len(self.small):
            val = heapq.heappop(self.large)
            heapq.heappush(self.small, -val)
    
    def findMedian(self) -> float:
        if len(self.small) > len(self.large):
            return -self.small[0]
        return (-self.small[0] + self.large[0]) / 2
```

---

## 📊 Visual Representation

```
Add 1: small=[-1], large=[]
       Median = 1

Add 2: small=[-1], large=[2]
       Median = (1+2)/2 = 1.5

Add 3: small=[-2,-1], large=[3]
       Actually: add 3→small, rebalance
       small=[-2], large=[3]
       Then add 1 more step...
       Median = 2
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| addNum | O(log n) | O(n) |
| findMedian | O(1) | - |

---

## 🎯 Key Takeaways

1. **Two heaps** - Split data at median
2. **Max heap in Python** - Negate values
3. **Balance sizes** - Differ by at most 1
4. **Median at tops** - O(1) access

---

## 🔗 Related Problems
- Sliding Window Median
- Kth Largest Element in a Stream
