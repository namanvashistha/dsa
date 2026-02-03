# Maximum Product Subarray

## 📋 Problem Statement

Given an integer array `nums`, find a subarray that has the largest product, and return the product.

### Examples

**Example 1:**
```
Input: nums = [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```

**Example 2:**
```
Input: nums = [-2,0,-1]
Output: 0
```

---

## 🧠 Thought Process

### Key Insight 💡
**Track both min and max!**
- Negative × negative = positive
- Current min could become max
- At each step: max = max(num, num×max, num×min)

---

## 💡 Solution

```python
def maxProduct(nums: list[int]) -> int:
    result = max(nums)
    curr_min, curr_max = 1, 1
    
    for num in nums:
        if num == 0:
            curr_min, curr_max = 1, 1
            continue
        
        temp = curr_max * num
        curr_max = max(num, temp, curr_min * num)
        curr_min = min(num, temp, curr_min * num)
        
        result = max(result, curr_max)
    
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Track min and max** - Both matter for products
2. **Reset on zero** - Can't extend through 0
3. **Three options** - Start fresh, extend max, extend min
4. **Initialize result carefully** - Handle all negatives

---

## 🔗 Related Problems
- Maximum Subarray (Kadane's)
- Product of Array Except Self
