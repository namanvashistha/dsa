# Sliding Window Maximum

## 📋 Problem Statement

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

### Examples

**Example 1:**
```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**Example 2:**
```
Input: nums = [1], k = 1
Output: [1]
```

### Constraints
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`
- `1 <= k <= nums.length`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Fixed-size window of k elements
- Find maximum in each window
- Total windows = n - k + 1

### Step 2: Brute Force
```python
# O(n * k) - too slow!
for i in range(n - k + 1):
    result.append(max(nums[i:i+k]))
```

### Step 3: Key Insight 💡
Use **Monotonic Decreasing Deque**:
- Store INDICES (not values) in deque
- Keep deque in decreasing order of values
- Front of deque = maximum of current window

**Why monotonic decreasing?**
- If nums[j] > nums[i] and j > i, then nums[i] can never be max
- Remove smaller elements from back when adding new element

---

## 💡 Solution

```python
from collections import deque

def maxSlidingWindow(nums: list[int], k: int) -> list[int]:
    result = []
    dq = deque()  # Store indices
    
    for i in range(len(nums)):
        # Remove indices outside current window from front
        while dq and dq[0] < i - k + 1:
            dq.popleft()
        
        # Remove smaller elements from back (maintain decreasing order)
        while dq and nums[dq[-1]] < nums[i]:
            dq.pop()
        
        # Add current index
        dq.append(i)
        
        # Add to result when window is complete (i >= k - 1)
        if i >= k - 1:
            result.append(nums[dq[0]])
    
    return result
```

---

## 🔍 Detailed Walkthrough

### Example: `nums = [1, 3, -1, -3, 5, 3, 6, 7], k = 3`

```
i=0, nums[0]=1:
  dq = [] → no cleanup needed
  dq = [0]
  Window not complete yet

i=1, nums[1]=3:
  dq[0]=0 ≥ 1-3+1=-1 ✓ (in window)
  nums[dq[-1]]=nums[0]=1 < 3 → pop 0
  dq = []
  dq = [1]
  Window not complete yet

i=2, nums[2]=-1:
  dq[0]=1 ≥ 2-3+1=0 ✓ (in window)
  nums[dq[-1]]=nums[1]=3 > -1 ✓ (keep)
  dq = [1, 2]
  Window complete! result = [nums[dq[0]]] = [3]

i=3, nums[3]=-3:
  dq[0]=1 ≥ 3-3+1=1 ✓ (in window)
  nums[dq[-1]]=nums[2]=-1 > -3 ✓ (keep)
  dq = [1, 2, 3]
  result = [3, nums[dq[0]]] = [3, 3]

i=4, nums[4]=5:
  dq[0]=1 ≥ 4-3+1=2 ✗ → popleft
  dq = [2, 3]
  dq[0]=2 ≥ 2 ✓
  nums[dq[-1]]=nums[3]=-3 < 5 → pop
  dq = [2]
  nums[dq[-1]]=nums[2]=-1 < 5 → pop
  dq = []
  dq = [4]
  result = [3, 3, 5]

i=5, nums[5]=3:
  dq[0]=4 ≥ 5-3+1=3 ✓
  nums[dq[-1]]=nums[4]=5 > 3 ✓
  dq = [4, 5]
  result = [3, 3, 5, 5]

i=6, nums[6]=6:
  dq[0]=4 ≥ 6-3+1=4 ✓
  nums[dq[-1]]=nums[5]=3 < 6 → pop
  dq = [4]
  nums[dq[-1]]=nums[4]=5 < 6 → pop
  dq = []
  dq = [6]
  result = [3, 3, 5, 5, 6]

i=7, nums[7]=7:
  dq[0]=6 ≥ 7-3+1=5 ✓
  nums[dq[-1]]=nums[6]=6 < 7 → pop
  dq = []
  dq = [7]
  result = [3, 3, 5, 5, 6, 7] ✓
```

---

## 📊 Visual Representation

```
nums = [1, 3, -1, -3, 5, 3, 6, 7], k = 3

Deque stores indices in decreasing order of values:

i=0: dq=[0]           values=[1]
i=1: dq=[1]           values=[3]        (1 popped, 3 > 1)
i=2: dq=[1,2]         values=[3,-1]     max=3 ✓
i=3: dq=[1,2,3]       values=[3,-1,-3]  max=3 ✓
i=4: dq=[4]           values=[5]        max=5 ✓ (all smaller popped)
i=5: dq=[4,5]         values=[5,3]      max=5 ✓
i=6: dq=[6]           values=[6]        max=6 ✓
i=7: dq=[7]           values=[7]        max=7 ✓

Result: [3, 3, 5, 5, 6, 7]
```

---

## 📊 Why Monotonic Deque Works

```
Window [1, 3, -1], k=3

If we keep all elements:
  When 3 enters, 1 can NEVER be max (3 is larger and entered later)
  Remove 1!

Maintain: larger elements on left, newer elements on right
If new element is larger → remove all smaller from right

deque[0] always has index of max (largest, and oldest if tie)
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(k) |

**Why O(n)?** Each element is added and removed from deque at most once.

---

## 🎯 Key Takeaways

1. **Monotonic decreasing deque** - Perfect for sliding window max
2. **Store indices, not values** - To check if index is within window
3. **Remove from front** - Index outside window
4. **Remove from back** - Smaller values (can't be max)

---

## ⚠️ Common Mistakes

1. Storing values instead of indices in deque
2. Not removing out-of-window indices from front
3. Using wrong comparison for removing from back
4. Adding to result before window is complete

---

## 🔄 Monotonic Deque Template

```python
from collections import deque

def monotonicDeque(nums, k):
    dq = deque()  # Store indices
    result = []
    
    for i in range(len(nums)):
        # Remove out-of-window from front
        while dq and dq[0] < i - k + 1:
            dq.popleft()
        
        # Maintain monotonic property from back
        while dq and nums[dq[-1]] < nums[i]:  # For decreasing
        # while dq and nums[dq[-1]] > nums[i]:  # For increasing
            dq.pop()
        
        dq.append(i)
        
        # Process when window is complete
        if i >= k - 1:
            result.append(nums[dq[0]])
    
    return result
```

---

## 🔗 Related Problems
- Daily Temperatures (monotonic stack)
- Shortest Subarray with Sum at Least K
- Constrained Subsequence Sum
- Longest Continuous Subarray With Absolute Diff ≤ Limit
