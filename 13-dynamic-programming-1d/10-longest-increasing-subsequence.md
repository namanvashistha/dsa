# Longest Increasing Subsequence

## 📋 Problem Statement

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

### Examples

**Example 1:**
```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: [2,3,7,101]
```

---

## 🧠 Thought Process

### Approaches:
1. **O(n²) DP** - For each position, check all previous
2. **O(n log n) Binary Search** - Maintain sorted subsequence

---

## 💡 Solution: DP

```python
def lengthOfLIS(nums: list[int]) -> int:
    n = len(nums)
    dp = [1] * n  # Each element is LIS of length 1
    
    for i in range(1, n):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)
    
    return max(dp)
```

## 💡 Solution: Binary Search

```python
import bisect

def lengthOfLIS(nums: list[int]) -> int:
    sub = []
    
    for num in nums:
        pos = bisect.bisect_left(sub, num)
        
        if pos == len(sub):
            sub.append(num)
        else:
            sub[pos] = num
    
    return len(sub)
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| DP | O(n²) | O(n) |
| Binary Search | O(n log n) | O(n) |

---

## 🎯 Key Takeaways

1. **DP O(n²)** - Check all previous elements
2. **Binary search O(n log n)** - Maintain smallest tail
3. **Binary search array ≠ actual LIS** - Just same length
4. **Strictly increasing** - Equal not allowed

---

## 🔗 Related Problems
- Number of Longest Increasing Subsequence
- Longest Increasing Subsequence II
