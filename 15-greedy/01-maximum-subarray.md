# Maximum Subarray (Kadane's Algorithm)

## 📋 Problem Statement

Given an integer array `nums`, find the subarray with the largest sum, and return its sum.

### Examples

**Example 1:**
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.
```

**Example 2:**
```
Input: nums = [5,4,-1,7,8]
Output: 23
```

---

## 🧠 Thought Process

### Key Insight: Kadane's Algorithm
At each position, decide:
- Start fresh from current element, OR
- Extend previous subarray

```
current = max(nums[i], current + nums[i])
```

If `current + nums[i] < nums[i]`, previous sum is negative → start fresh!

---

## 💡 Solution

```python
def maxSubArray(nums: list[int]) -> int:
    max_sum = nums[0]
    current = nums[0]
    
    for i in range(1, len(nums)):
        current = max(nums[i], current + nums[i])
        max_sum = max(max_sum, current)
    
    return max_sum
```

---

## 🔍 Detailed Walkthrough

```
nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

i=0: current=-2, max_sum=-2
i=1: current=max(1, -2+1)=1, max_sum=1
i=2: current=max(-3, 1-3)=-2, max_sum=1
i=3: current=max(4, -2+4)=4, max_sum=4
i=4: current=max(-1, 4-1)=3, max_sum=4
i=5: current=max(2, 3+2)=5, max_sum=5
i=6: current=max(1, 5+1)=6, max_sum=6 ⭐
i=7: current=max(-5, 6-5)=1, max_sum=6
i=8: current=max(4, 1+4)=5, max_sum=6

Result: 6 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Kadane's Algorithm** - Greedy/DP hybrid
2. **Drop negative prefix** - Start fresh if sum negative
3. **Track running and global max** - Two variables
4. **One pass solution** - Elegant and efficient

---

## 🔗 Related Problems
- Maximum Product Subarray
- Best Time to Buy and Sell Stock
- Maximum Sum Circular Subarray
