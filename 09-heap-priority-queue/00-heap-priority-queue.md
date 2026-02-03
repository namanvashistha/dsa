# 🔺 Heap / Priority Queue - NeetCode 150

> 7 problems | Master min/max heaps and K-based problems

---

## 1️⃣ Kth Largest Element in Stream ⭐ Easy
**The Trick:** Min heap of size k
- Keep only k largest elements in heap
- Top of min heap = kth largest
- New element > top? → replace
- **Remember:** Min heap of size k for kth largest

---

## 2️⃣ Last Stone Weight ⭐ Easy
**The Trick:** Max heap, smash two heaviest
- Use max heap (negate values for Python)
- Pop two largest
- If different, push difference back
- **Remember:** Max heap for largest elements

---

## 3️⃣ K Closest Points to Origin ⭐⭐ Medium
**The Trick:** Max heap of size k by distance
- Calculate distance: `x² + y²` (skip sqrt)
- Keep k smallest in max heap
- Heap top = kth closest, bigger gets removed
- **Remember:** Max heap of size k for k smallest

---

## 4️⃣ Kth Largest Element in Array ⭐⭐ Medium
**The Trick:** Min heap of size k OR quickselect
- **Heap:** Keep k largest in min heap
- **Quickselect:** O(n) average, O(n²) worst
- **Remember:** Min heap size k or partition-based

---

## 5️⃣ Task Scheduler ⭐⭐ Medium
**The Trick:** Max heap + cooldown queue
- Use max heap for task frequencies
- After executing, add to cooldown queue
- After n cycles, add back to heap
- **Remember:** Heap for most frequent + queue for cooling

---

## 6️⃣ Design Twitter ⭐⭐ Medium
**The Trick:** Merge k sorted lists (feeds)
- Each user has list of tweets (newest first)
- Merge using min heap
- Heap stores (timestamp, tweet, user, index)
- **Remember:** Merge feeds using heap

---

## 7️⃣ Find Median from Data Stream ⭐⭐⭐ Hard
**The Trick:** Two heaps (max for small, min for large)
- Max heap: smaller half (left)
- Min heap: larger half (right)
- Keep sizes balanced (differ by at most 1)
- Median = middle element(s)
- **Remember:** Two heaps split the data

**Structure:**
```
small (max heap) | large (min heap)
     [3, 2, 1]   |   [4, 5, 6]
         ↑       |       ↑
      max=3      |    min=4
         median = (3+4)/2
```

---

## 🎯 Pattern Recognition

**Use Heap when:**
- Find kth largest/smallest
- Maintain top k elements
- Merge k sorted lists
- Need repeated min/max access
- Task scheduling with priorities

**Heap Types:**
- **Min Heap:** Smallest element at top
- **Max Heap:** Largest element at top

**K Problems Strategy:**
- **Kth Largest:** Use min heap of size k
- **Kth Smallest:** Use max heap of size k
- **Top K:** Keep k elements in heap

**Common Patterns:**

1. **Kth Element Pattern:**
```python
heap = []
for num in nums:
    heappush(heap, num)  # min heap for kth largest
    if len(heap) > k:
        heappop(heap)
return heap[0]  # kth largest
```

2. **Two Heaps (Median):**
```python
small = []  # max heap (negate values)
large = []  # min heap

# Keep small.size == large.size or small.size = large.size + 1
# Median = top of small (if odd) or avg of both tops
```

3. **Merge K Lists:**
```python
heap = [(lists[i][0], i, 0) for i in range(k)]
heapify(heap)

while heap:
    val, list_idx, elem_idx = heappop(heap)
    result.append(val)
    if elem_idx + 1 < len(lists[list_idx]):
        heappush(heap, (lists[list_idx][elem_idx+1], list_idx, elem_idx+1))
```

**Time Complexity:**
- Insert: O(log n)
- Extract min/max: O(log n)
- Peek min/max: O(1)
- Build heap: O(n)

**Python Heapq (Min Heap):**
```python
import heapq

heapq.heappush(heap, item)
heapq.heappop(heap)
heapq.heapify(list)  # in-place

# Max heap trick
heapq.heappush(heap, -item)  # negate
max_item = -heapq.heappop(heap)  # negate back
```

**Common Mistakes:**
- Using max heap for kth largest (should be min heap!)
- Forgetting to negate for max heap in Python
- Not maintaining heap property after modifications
- Comparing wrong heap sizes in two-heap problems

**Key Insights:**
- Kth largest = min heap of size k (counterintuitive!)
- Two heaps = split data, O(1) median
- Heap = better than sorting when k << n
- Merge k sorted = heap of k elements, not n

**Complexity Decision:**
- Find k elements: Heap O(n log k) vs Sort O(n log n)
- If k << n → heap wins
- If need all sorted → just sort
