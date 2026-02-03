# Find Minimum in Rotated Sorted Array

## 📋 Problem Statement

Given a sorted rotated array of unique elements, return the minimum element.

You must write an algorithm that runs in `O(log n)` time.

### Examples

**Example 1:**
```
Input: nums = [3,4,5,1,2]
Output: 1
```

**Example 2:**
```
Input: nums = [4,5,6,7,0,1,2]
Output: 0
```

---

## 🧠 Thought Process

### Key Insight 💡
The minimum is where the rotation point is!
- Compare mid with right
- If mid > right: min is in right half
- If mid < right: min is in left half (including mid)

---

## 💡 Solution

```python
def findMin(nums: list[int]) -> int:
    left, right = 0, len(nums) - 1
    
    while left < right:
        mid = (left + right) // 2
        
        if nums[mid] > nums[right]:
            # Min is in right half
            left = mid + 1
        else:
            # Min is in left half (could be mid)
            right = mid
    
    return nums[left]
```

---

## 🔍 Detailed Walkthrough

```
nums = [4, 5, 6, 7, 0, 1, 2]

left=0, right=6, mid=3: nums[3]=7 > nums[6]=2
  Min in right → left=4

left=4, right=6, mid=5: nums[5]=1 < nums[6]=2
  Min in left → right=5

left=4, right=5, mid=4: nums[4]=0 < nums[5]=1
  Min in left → right=4

left=4, right=4: Done!

Result: nums[4] = 0 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(log n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Compare with right, not left** - Handles rotation
2. **left < right** - Not <=, converge to minimum
3. **right = mid** - Don't skip potential minimum
4. **left = mid + 1** - mid is not the min

---

## 🔗 Related Problems
- Find Minimum in Rotated Sorted Array II (duplicates)
- Search in Rotated Sorted Array
