# Median of Two Sorted Arrays

## 📋 Problem Statement

Given two sorted arrays `nums1` and `nums2` of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity should be `O(log (m+n))`.

### Examples

**Example 1:**
```
Input: nums1 = [1,3], nums2 = [2]
Output: 2.0
Explanation: merged = [1,2,3], median = 2
```

**Example 2:**
```
Input: nums1 = [1,2], nums2 = [3,4]
Output: 2.5
Explanation: merged = [1,2,3,4], median = (2+3)/2 = 2.5
```

---

## 🧠 Thought Process

### Key Insight 💡
Binary search on the smaller array to find the partition:
- Left partition: half of total elements
- All elements in left ≤ all elements in right
- Median is at the partition boundary

---

## 💡 Solution

```python
def findMedianSortedArrays(nums1: list[int], nums2: list[int]) -> float:
    # Ensure nums1 is smaller
    if len(nums1) > len(nums2):
        nums1, nums2 = nums2, nums1
    
    m, n = len(nums1), len(nums2)
    total = m + n
    half = total // 2
    
    left, right = 0, m
    
    while left <= right:
        i = (left + right) // 2  # Partition in nums1
        j = half - i             # Partition in nums2
        
        # Edge cases: use infinity for out of bounds
        nums1_left = nums1[i - 1] if i > 0 else float('-inf')
        nums1_right = nums1[i] if i < m else float('inf')
        nums2_left = nums2[j - 1] if j > 0 else float('-inf')
        nums2_right = nums2[j] if j < n else float('inf')
        
        # Check if valid partition
        if nums1_left <= nums2_right and nums2_left <= nums1_right:
            # Found correct partition
            if total % 2 == 1:
                return min(nums1_right, nums2_right)
            else:
                return (max(nums1_left, nums2_left) + 
                        min(nums1_right, nums2_right)) / 2
        elif nums1_left > nums2_right:
            right = i - 1
        else:
            left = i + 1
    
    return 0.0
```

---

## 📊 Visual Explanation

```
nums1 = [1, 3, 5]
nums2 = [2, 4, 6, 8]

Total = 7, half = 3 (need 3 on left for odd total)

Partition:
nums1: [1] | [3, 5]
nums2: [2, 4] | [6, 8]

Left: [1, 2, 4] → max = 4
Right: [3, 5, 6, 8] → min = 3

4 > 3? Invalid! Move partition left in nums2.

Eventually: median = 4
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(log(min(m,n))) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Binary search on smaller array** - O(log min(m,n))
2. **Partition to get half elements** - Key insight
3. **Valid partition** - left max ≤ right min
4. **Handle edges with infinity** - Clean code

---

## 🔗 Related Problems
- Merge Sorted Array
- Find K-th Smallest Element in Two Sorted Arrays
