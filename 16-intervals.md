# ⏰ Intervals - NeetCode 150

> 6 problems | Master interval manipulation and scheduling

---

## 1️⃣ Insert Interval ⭐⭐ Medium
**The Trick:** Three phases - before, merge, after
- Add all intervals ending before new starts
- Merge all overlapping with new interval
- Add all intervals starting after new ends
- **Remember:** Before → merge → after

---

## 2️⃣ Merge Intervals ⭐⭐ Medium
**The Trick:** Sort by start, merge overlapping
- Sort intervals by start time
- If current overlaps last → extend last's end
- Else → add as new interval
- **Remember:** `overlap if start ≤ last_end`

---

## 3️⃣ Non-overlapping Intervals ⭐⭐ Medium
**The Trick:** Sort by end, greedily keep earliest ending
- Sort by end time
- Keep interval with earliest end
- Count/remove overlapping ones
- **Remember:** Keep earliest ending → more room for future

---

## 4️⃣ Meeting Rooms ⭐ Easy
**The Trick:** Sort and check consecutive overlap
- Sort by start time
- Check if any meeting starts before previous ends
- **Remember:** Just check adjacent after sorting

---

## 5️⃣ Meeting Rooms II ⭐⭐ Medium
**The Trick:** Min heap for ongoing meetings
- Sort by start time
- Use min heap tracking end times
- When new starts, remove finished meetings
- Heap size = rooms needed
- **Remember:** Heap tracks active meetings

**Alternative:** Start/end arrays, two pointers

---

## 6️⃣ Minimum Interval to Include Each Query ⭐⭐⭐ Hard
**The Trick:** Sort intervals and queries, use heap
- Sort intervals by start, queries by value
- For each query, add all valid intervals to heap
- Remove invalid intervals (end < query)
- Heap top = minimum interval size
- **Remember:** Process queries in sorted order with heap

---

## 🎯 Pattern Recognition

**Interval Representation:**
- `[start, end]` - inclusive or exclusive (be consistent!)
- Sometimes `(start, end, value/id)`

**Overlap Conditions:**
- **Overlapping:** `start1 ≤ end2 AND start2 ≤ end1`
- **Simple check:** `max(start1, start2) < min(end1, end2)`
- **After sorting:** just check `start_current ≤ end_previous`

**Common Operations:**

1. **Merge two intervals:**
```python
merged = [min(start1, start2), max(end1, end2)]
```

2. **Check overlap:**
```python
def overlaps(i1, i2):
    return i1[0] <= i2[1] and i2[0] <= i1[1]
```

3. **Sort intervals:**
```python
intervals.sort()  # By start time
intervals.sort(key=lambda x: x[1])  # By end time
```

**Sort By Start vs End:**

**Sort by Start:**
- Merge intervals
- Insert interval
- Check if can attend all meetings
- Most general-purpose approach

**Sort by End:**
- Maximum non-overlapping intervals
- Minimum removals to make non-overlapping
- Greedy scheduling

**Pattern Templates:**

### 1. Merge Intervals
```python
intervals.sort()
merged = [intervals[0]]

for current in intervals[1:]:
    if current[0] <= merged[-1][1]:
        # Overlap - merge
        merged[-1][1] = max(merged[-1][1], current[1])
    else:
        # No overlap - add new
        merged.append(current)
```

### 2. Count Overlapping (Min Rooms)
```python
starts = sorted([i[0] for i in intervals])
ends = sorted([i[1] for i in intervals])

rooms = max_rooms = 0
s = e = 0

while s < len(starts):
    if starts[s] < ends[e]:
        rooms += 1
        max_rooms = max(max_rooms, rooms)
        s += 1
    else:
        rooms -= 1
        e += 1
```

### 3. Greedy Selection (Max Non-overlapping)
```python
intervals.sort(key=lambda x: x[1])  # Sort by end
count = 0
end = float('-inf')

for start, finish in intervals:
    if start >= end:  # No overlap
        count += 1
        end = finish
```

**Time Complexity:**
- Sort: O(n log n)
- Scan: O(n)
- With heap: O(n log n)
- Total: usually O(n log n)

**Space Complexity:**
- Merged result: O(n)
- Heap: O(n) worst case

**Common Mistakes:**
- Wrong overlap condition (off-by-one)
- Not sorting before processing
- Sorting by wrong attribute (start vs end)
- Forgetting inclusive/exclusive endpoints
- Not handling empty intervals list
- Modifying while iterating

**Edge Cases to Consider:**
- Empty list of intervals
- Single interval
- All intervals overlap (become one)
- No intervals overlap (all separate)
- Point intervals `[x, x]`
- Intervals in reverse order

**Key Insights:**
- **Sort first** - makes most problems easier
- **Merge:** Sort by start, check adjacent
- **Non-overlapping:** Sort by end, greedy keep
- **Rooms needed:** Track concurrent meetings
- Heap useful for dynamic interval tracking
- Two pointers useful for start/end arrays

**Pattern Recognition:**
- "Merge" → sort by start
- "Maximum non-overlapping" → sort by end
- "How many rooms/resources" → heap or two arrays
- "Insert/update" → three phases approach
- "Query intervals" → sort queries + heap

**Visualization Tip:**
Draw timeline:
```
Time: 0   1   2   3   4   5   6   7   8
      |---|====|===|       |---|
          |========|   |=======|
              |---|       |---|
```
Helps see overlaps and merges!

**Related Problems:**
- Scheduling meetings
- Resource allocation
- Timeline merging
- Range queries
- Event processing

**Decision Tree:**
1. Need to merge? → Sort by start
2. Need max non-overlapping? → Sort by end
3. Need room count? → Heap or two arrays
4. Need to query? → Sort both + heap
