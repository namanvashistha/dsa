# Meeting Rooms

## 📋 Problem Statement

Given an array of meeting time intervals `intervals` where `intervals[i] = [starti, endi]`, determine if a person could attend all meetings.

### Examples

**Example 1:**
```
Input: intervals = [[0,30],[5,10],[15,20]]
Output: false
```

**Example 2:**
```
Input: intervals = [[7,10],[2,4]]
Output: true
```

---

## 💡 Solution

```python
def canAttendMeetings(intervals: list[list[int]]) -> bool:
    intervals.sort(key=lambda x: x[0])
    
    for i in range(1, len(intervals)):
        if intervals[i][0] < intervals[i-1][1]:
            return False
    
    return True
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n log n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Sort by start time**
2. **Check adjacent pairs** - For overlap
3. **Return false on first overlap**
4. **Base case for intervals** - Overlap detection

---

## 🔗 Related Problems
- Meeting Rooms II
- Merge Intervals
