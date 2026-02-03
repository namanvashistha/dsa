# Meeting Rooms II

## 📋 Problem Statement

Given an array of meeting time intervals `intervals` where `intervals[i] = [starti, endi]`, return the minimum number of conference rooms required.

### Examples

**Example 1:**
```
Input: intervals = [[0,30],[5,10],[15,20]]
Output: 2
```

**Example 2:**
```
Input: intervals = [[7,10],[2,4]]
Output: 1
```

---

## 🧠 Thought Process

### Key Insight 💡
Track overlapping meetings at any point in time.

**Approach 1: Min Heap**
- Sort by start time
- Heap stores end times of ongoing meetings
- If new meeting starts after heap top ends, reuse room

**Approach 2: Event-based**
- Track start/end events separately
- Count concurrent meetings

---

## 💡 Solution: Min Heap

```python
import heapq

def minMeetingRooms(intervals: list[list[int]]) -> int:
    if not intervals:
        return 0
    
    intervals.sort(key=lambda x: x[0])
    heap = []  # End times
    
    for start, end in intervals:
        # If earliest ending meeting has ended
        if heap and heap[0] <= start:
            heapq.heappop(heap)
        
        heapq.heappush(heap, end)
    
    return len(heap)
```

## 💡 Solution: Two Pointers

```python
def minMeetingRooms(intervals: list[list[int]]) -> int:
    starts = sorted([i[0] for i in intervals])
    ends = sorted([i[1] for i in intervals])
    
    rooms = 0
    end_ptr = 0
    
    for start in starts:
        if start < ends[end_ptr]:
            rooms += 1
        else:
            end_ptr += 1
    
    return rooms
```

---

## 🔍 Detailed Walkthrough

```
intervals = [[0,30], [5,10], [15,20]]
Sorted by start: [[0,30], [5,10], [15,20]]

[0,30]: heap empty → push 30, heap=[30]
[5,10]: 30 > 5 → need new room, push 10, heap=[10,30]
[15,20]: 10 <= 15 → reuse room, pop 10, push 20, heap=[20,30]

Rooms needed: 2 ✓
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Min Heap | O(n log n) | O(n) |
| Two Pointers | O(n log n) | O(n) |

---

## 🎯 Key Takeaways

1. **Heap tracks end times** - Pop when room freed
2. **Sort by start** - Process chronologically
3. **Heap size = rooms** - Concurrent meetings
4. **Alternative: sweep line** - Event-based

---

## 🔗 Related Problems
- Meeting Rooms I (check overlap)
- Merge Intervals
- Car Pooling
