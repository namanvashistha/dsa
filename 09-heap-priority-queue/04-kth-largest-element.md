# Kth Largest Element in an Array

## 📋 Problem Statement

Given an integer array `nums` and an integer `k`, return the `k`th largest element in the array.

Note that it is the `k`th largest element in the sorted order, not the `k`th distinct element.

Can you solve it without sorting?

### Examples

**Example 1:**
```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```

**Example 2:**
```
Input: nums = [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

---

## 🧠 Thought Process

### Approaches
1. **Sort:** O(n log n) - simple but not optimal
2. **Min Heap of size k:** O(n log k) - good!
3. **QuickSelect:** O(n) average - optimal!

---

## 💡 Solution: Min Heap

```python
import heapq

def findKthLargest(nums: list[int], k: int) -> int:
    # Keep min heap of size k
    heap = []
    
    for num in nums:
        heapq.heappush(heap, num)
        if len(heap) > k:
            heapq.heappop(heap)  # Remove smallest
    
    return heap[0]  # Kth largest = smallest of k largest
```

## 💡 Solution: QuickSelect

```python
import random

def findKthLargest(nums: list[int], k: int) -> int:
    k = len(nums) - k  # Convert to kth smallest
    
    def quickselect(l, r):
        pivot = nums[r]
        p = l
        
        for i in range(l, r):
            if nums[i] <= pivot:
                nums[p], nums[i] = nums[i], nums[p]
                p += 1
        
        nums[p], nums[r] = nums[r], nums[p]
        
        if p < k:
            return quickselect(p + 1, r)
        elif p > k:
            return quickselect(l, p - 1)
        else:
            return nums[p]
    
    return quickselect(0, len(nums) - 1)
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Sort | O(n log n) | O(1) |
| Min Heap | O(n log k) | O(k) |
| QuickSelect | O(n) avg | O(1) |

---

## 🎯 Key Takeaways

1. **Min heap of size k** - Top k largest, pop smallest
2. **QuickSelect** - Partition like quicksort, recurse on one side
3. **k conversion** - Kth largest = (n-k)th smallest
4. **Random pivot** - Avoid worst case O(n²)

---

## 🔗 Related Problems
- Top K Frequent Elements
- K Closest Points to Origin
- Find Median from Data Stream
