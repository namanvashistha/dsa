# Insert Interval

## 📋 Problem Statement

You are given an array of non-overlapping intervals `intervals` where `intervals[i] = [starti, endi]` sorted in ascending order by `starti`. You are also given an interval `newInterval`.

Insert `newInterval` into `intervals` such that `intervals` is still sorted and non-overlapping.

### Examples

**Example 1:**
```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```

---

## 💡 Solution

```python
def insert(intervals: list[list[int]], newInterval: list[int]) -> list[list[int]]:
    result = []
    
    for i, interval in enumerate(intervals):
        if newInterval[1] < interval[0]:
            # New interval ends before current starts
            result.append(newInterval)
            return result + intervals[i:]
        
        elif newInterval[0] > interval[1]:
            # New interval starts after current ends
            result.append(interval)
        
        else:
            # Overlapping - merge
            newInterval = [
                min(newInterval[0], interval[0]),
                max(newInterval[1], interval[1])
            ]
    
    result.append(newInterval)
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Three cases** - Before, after, overlapping
2. **Merge on overlap** - Update newInterval
3. **Early return** - When no more overlaps possible
4. **Add merged at end** - If not returned early

---

## 🔗 Related Problems
- Merge Intervals
- Non-overlapping Intervals
