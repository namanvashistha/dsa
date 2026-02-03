# Search in Rotated Sorted Array

## 📋 Problem Statement

Given the array `nums` after the possible rotation and an integer `target`, return the index of `target` if it is in `nums`, or `-1` if it is not in `nums`.

You must write an algorithm with `O(log n)` runtime complexity.

### Examples

**Example 1:**
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

**Example 2:**
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

---

## 🧠 Thought Process

### Key Insight 💡
After rotation, one half is always sorted!
- Check which half is sorted
- Check if target is in that sorted half
- Eliminate half

---

## 💡 Solution

```python
def search(nums: list[int], target: int) -> int:
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if nums[mid] == target:
            return mid
        
        # Left half is sorted
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # Right half is sorted
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    
    return -1
```

---

## 🔍 Detailed Walkthrough

```
nums = [4, 5, 6, 7, 0, 1, 2], target = 0

left=0, right=6, mid=3: nums[3]=7
  Left [4,5,6,7] sorted
  0 not in [4,7) → search right
  left = 4

left=4, right=6, mid=5: nums[5]=1
  Left [0,1] sorted? nums[4]=0 <= nums[5]=1 ✓
  0 in [0,1)? 0 >= 0 and 0 < 1 ✓
  right = 4

left=4, right=4, mid=4: nums[4]=0 == target ✓

Result: 4 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(log n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **One half always sorted** - Key observation!
2. **Check sorted half first** - Determine target's location
3. **Handle edge cases** - `nums[left] <= nums[mid]` (not <)
4. **Modified binary search** - Same template

---

## 🔗 Related Problems
- Find Minimum in Rotated Sorted Array
- Search in Rotated Sorted Array II (duplicates)
- Find Peak Element
