# Non-overlapping Intervals

## 📋 Problem Statement

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

### Examples

**Example 1:**
```
Input: intervals = [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: Remove [1,3] to make [[1,2],[2,3],[3,4]] non-overlapping.
```

---

## 🧠 Thought Process

### Key Insight 💡
**Greedy: Keep intervals that end earliest!**
- Sort by end time
- If overlap, remove the one that ends later (keep current)
- If no overlap, keep both

---

## 💡 Solution

```python
def eraseOverlapIntervals(intervals: list[list[int]]) -> int:
    intervals.sort(key=lambda x: x[1])
    
    count = 0
    prev_end = float('-inf')
    
    for start, end in intervals:
        if start >= prev_end:
            # No overlap - keep this interval
            prev_end = end
        else:
            # Overlap - remove this interval (count it)
            count += 1
    
    return count
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n log n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Sort by end time** - Key insight
2. **Greedy selection** - Keep earliest ending
3. **Count removals** - Overlapping intervals
4. **Similar to activity selection**

---

## 🔗 Related Problems
- Merge Intervals
- Minimum Number of Arrows to Burst Balloons
