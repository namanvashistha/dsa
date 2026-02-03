# Binary Search

## 📋 Problem Statement

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`.

You must write an algorithm with **O(log n)** runtime complexity.

### Examples

**Example 1:**
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

**Example 2:**
```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

### Constraints
- `1 <= nums.length <= 10^4`
- `-10^4 < nums[i], target < 10^4`
- All integers in `nums` are **unique**
- `nums` is sorted in ascending order

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Sorted array → binary search!
- Find target or return -1
- Must be O(log n)

### Step 2: Binary Search Logic
1. Look at middle element
2. If target → found!
3. If target < mid → search left half
4. If target > mid → search right half
5. Repeat until found or search space empty

---

## 💡 Solution

```python
def search(nums: list[int], target: int) -> int:
    left = 0
    right = len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2  # Avoid overflow
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1
```

---

## 🔍 Detailed Walkthrough

### Example: `nums = [-1, 0, 3, 5, 9, 12], target = 9`

```
Initial: left=0, right=5

Iteration 1:
  mid = (0 + 5) // 2 = 2
  nums[2] = 3 < 9
  target in right half → left = 3

Iteration 2:
  mid = (3 + 5) // 2 = 4
  nums[4] = 9 == 9 ✓
  Return 4

Result: 4 ✓
```

---

## 📊 Visual Representation

```
nums = [-1, 0, 3, 5, 9, 12], target = 9

Step 1:
[-1, 0, 3, 5, 9, 12]
  L     M        R
        ↑
     3 < 9, search right

Step 2:
[-1, 0, 3, 5, 9, 12]
           L  M   R
              ↑
           9 == 9, Found!
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(log n) |
| Space | O(1) |

Each iteration eliminates half the search space.

---

## 🎯 Key Takeaways

1. **Sorted array = Binary Search** - Always consider!
2. **mid = left + (right - left) // 2** - Prevents overflow
3. **left <= right** - Include equal for single element
4. **Update left = mid + 1 or right = mid - 1** - Avoid infinite loop

---

## 🔗 Related Problems
- Search Insert Position
- Find First and Last Position
- Search in Rotated Sorted Array
- Koko Eating Bananas (Binary Search on Answer)
