# Last Stone Weight

## 📋 Problem Statement

You are given an array of integers `stones` where `stones[i]` is the weight of the `ith` stone.

Each turn, we choose the **two heaviest** stones and smash them. If `x <= y`:
- If `x == y`, both are destroyed
- If `x != y`, stone of weight `y - x` remains

Return the weight of the last remaining stone, or `0` if there are none.

### Examples

**Example 1:**
```
Input: stones = [2,7,4,1,8,1]
Output: 1
Explanation:
8 vs 7 → 1 remains
4 vs 2 → 2 remains
2 vs 1 → 1 remains
1 vs 1 → both destroyed
1 remains
```

---

## 💡 Solution

```python
import heapq

def lastStoneWeight(stones: list[int]) -> int:
    # Max heap (negate values)
    heap = [-s for s in stones]
    heapq.heapify(heap)
    
    while len(heap) > 1:
        first = -heapq.heappop(heap)
        second = -heapq.heappop(heap)
        
        if first != second:
            heapq.heappush(heap, -(first - second))
    
    return -heap[0] if heap else 0
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n log n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Max heap needed** - Negate values in Python
2. **Pop two, potentially push one** - Simulation
3. **Continue until 1 or 0** - Return result

---

## 🔗 Related Problems
- Last Stone Weight II (DP)
