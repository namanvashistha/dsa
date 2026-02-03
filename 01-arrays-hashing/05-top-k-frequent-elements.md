# Top K Frequent Elements

## 📋 Problem Statement

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order.

### Examples

**Example 1:**
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Explanation: 1 appears 3 times, 2 appears 2 times
```

**Example 2:**
```
Input: nums = [1], k = 1
Output: [1]
```

### Constraints
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `k` is in the range `[1, number of unique elements]`
- Answer is guaranteed to be unique

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Count frequency of each element
- Find k elements with highest frequencies
- Order in output doesn't matter

### Step 2: Break Into Sub-Problems
1. **Count frequencies** → HashMap
2. **Find top k** → Sorting or Heap or Bucket Sort

### Step 3: Consider Approaches

| Approach | Step 1 | Step 2 | Time | Space |
|----------|--------|--------|------|-------|
| Sort | O(n) count | O(n log n) sort | O(n log n) | O(n) |
| Heap | O(n) count | O(n log k) heap | O(n log k) | O(n) |
| Bucket Sort | O(n) count | O(n) bucket | O(n) | O(n) |

---

## 💡 Solution Approaches

### Approach 1: Sorting (Simple)

```python
from collections import Counter

def topKFrequent(nums: list[int], k: int) -> list[int]:
    # Count frequencies
    count = Counter(nums)
    
    # Sort by frequency (descending) and take first k
    sorted_elements = sorted(count.keys(), key=lambda x: count[x], reverse=True)
    
    return sorted_elements[:k]
```

### Approach 2: Min Heap of Size K

```python
import heapq
from collections import Counter

def topKFrequent(nums: list[int], k: int) -> list[int]:
    # Count frequencies
    count = Counter(nums)
    
    # Use min heap of size k
    # Heap contains (frequency, element)
    heap = []
    
    for num, freq in count.items():
        heapq.heappush(heap, (freq, num))
        
        if len(heap) > k:
            heapq.heappop(heap)  # Remove smallest frequency
    
    return [num for freq, num in heap]
```

**Why Min Heap?**
- We want TOP k (highest frequencies)
- Min heap removes SMALLEST
- Keep pushing, pop when size > k
- Result: k largest remain in heap

### Approach 3: Bucket Sort (Optimal) ⭐

```python
from collections import Counter

def topKFrequent(nums: list[int], k: int) -> list[int]:
    # Count frequencies
    count = Counter(nums)
    
    # Create buckets where index = frequency
    # Maximum frequency possible = len(nums)
    buckets = [[] for _ in range(len(nums) + 1)]
    
    for num, freq in count.items():
        buckets[freq].append(num)
    
    # Collect from highest frequency buckets
    result = []
    for freq in range(len(buckets) - 1, 0, -1):
        for num in buckets[freq]:
            result.append(num)
            if len(result) == k:
                return result
    
    return result
```

**Walkthrough with Example:** `nums = [1,1,1,2,2,3], k = 2`
```
Step 1: Count frequencies
count = {1: 3, 2: 2, 3: 1}

Step 2: Create buckets (index = frequency)
buckets[0] = []
buckets[1] = [3]      # frequency 1
buckets[2] = [2]      # frequency 2
buckets[3] = [1]      # frequency 3
buckets[4] = []
buckets[5] = []
buckets[6] = []

Step 3: Collect from highest frequency
freq=6: empty
freq=5: empty
freq=4: empty
freq=3: add 1, result=[1]
freq=2: add 2, result=[1,2], len=k=2 → return!

Result: [1, 2] ✓
```

---

## 🔍 Why Bucket Sort Works

**Key Insight:** The maximum possible frequency is `n` (length of array).

- Create `n+1` buckets (indices 0 to n)
- Each bucket holds elements with that frequency
- Walk from highest index (frequency) to lowest
- Pick elements until we have k

This gives us O(n) time because:
- O(n) to count
- O(n) to fill buckets (each element counted once)
- O(n) to collect (visit each bucket at most once)

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Sorting | O(n log n) | O(n) |
| Min Heap | O(n log k) | O(n + k) |
| Bucket Sort | O(n) | O(n) |

---

## 🎯 Key Takeaways

1. **Count first, then find top k** - Two-step process
2. **Min heap for top k** - Counterintuitive but works!
3. **Bucket sort when range is bounded** - Frequency ≤ n
4. **Trade time for space** - Bucket sort uses more space but faster

---

## ⚠️ Common Mistakes

1. Using max heap incorrectly (heapify all, pop k times = O(n + k log n))
2. Forgetting that Python's heapq is min heap only
3. Not handling single element case

---

## 💡 Heap Trick: Max Heap in Python

```python
# Python only has min heap, so negate values for max heap
import heapq

# Max heap simulation
max_heap = []
heapq.heappush(max_heap, -5)  # Store negated
heapq.heappush(max_heap, -3)
heapq.heappush(max_heap, -8)

largest = -heapq.heappop(max_heap)  # Negate back: 8
```

---

## 🔗 Related Problems
- Kth Largest Element in an Array
- Sort Characters By Frequency
- Top K Frequent Words
- K Closest Points to Origin
