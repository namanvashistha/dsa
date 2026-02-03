# Merge Intervals

## 📋 Problem Statement

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

### Examples

**Example 1:**
```
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: [1,3] and [2,6] overlap, merged to [1,6]
```

**Example 2:**
```
Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
```

---

## 🧠 Thought Process

### Step 1: Sort by Start Time
After sorting, overlapping intervals are adjacent!

### Step 2: Merge Logic
If current starts before previous ends → merge (extend end)
Otherwise → new interval

---

## 💡 Solution

```python
def merge(intervals: list[list[int]]) -> list[list[int]]:
    intervals.sort(key=lambda x: x[0])
    merged = [intervals[0]]
    
    for start, end in intervals[1:]:
        if start <= merged[-1][1]:
            # Overlap: extend end
            merged[-1][1] = max(merged[-1][1], end)
        else:
            # No overlap: add new interval
            merged.append([start, end])
    
    return merged
```

---

## 🔍 Detailed Walkthrough

```
intervals = [[1,3],[2,6],[8,10],[15,18]]

After sort: [[1,3],[2,6],[8,10],[15,18]]

merged = [[1,3]]

[2,6]: 2 ≤ 3? Yes! merged = [[1,6]]
[8,10]: 8 ≤ 6? No! merged = [[1,6],[8,10]]
[15,18]: 15 ≤ 10? No! merged = [[1,6],[8,10],[15,18]]

Result: [[1,6],[8,10],[15,18]] ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n log n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Sort first** - Makes overlaps adjacent
2. **Extend or add** - Simple merge logic
3. **Check start ≤ previous end** - Overlap condition
4. **Classic interval pattern**

---

## 🔗 Related Problems
- Insert Interval
- Non-overlapping Intervals
- Meeting Rooms I & II
