# Minimum Interval to Include Each Query

## 📋 Problem Statement

You are given a 2D array `intervals` where `intervals[i] = [lefti, righti]` represents the `ith` interval starting at `lefti` and ending at `righti` (inclusive).

You are given an integer array `queries`. The answer to the `jth` query is the size of the smallest interval `i` such that `lefti <= queries[j] <= righti`. If no such interval exists, the answer is `-1`.

Return an array containing the answers to the queries.

### Examples

**Example 1:**
```
Input: intervals = [[1,4],[2,4],[3,6],[4,4]], queries = [2,3,4,5]
Output: [3,3,1,4]
```

---

## 💡 Solution

```python
import heapq

def minInterval(intervals: list[list[int]], queries: list[int]) -> list[int]:
    intervals.sort()
    sorted_queries = sorted(enumerate(queries), key=lambda x: x[1])
    
    result = [-1] * len(queries)
    heap = []  # (size, right)
    i = 0
    
    for idx, q in sorted_queries:
        # Add all intervals that start <= q
        while i < len(intervals) and intervals[i][0] <= q:
            left, right = intervals[i]
            heapq.heappush(heap, (right - left + 1, right))
            i += 1
        
        # Remove intervals that end before q
        while heap and heap[0][1] < q:
            heapq.heappop(heap)
        
        if heap:
            result[idx] = heap[0][0]
    
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O((n + m) log n) |
| Space | O(n + m) |

---

## 🎯 Key Takeaways

1. **Sort both** - Process in order
2. **Min heap by size** - Track smallest valid interval
3. **Lazy removal** - Remove expired intervals when needed
4. **Preserve query order** - Store original indices

---

## 🔗 Related Problems
- Meeting Rooms II
- Merge Intervals
