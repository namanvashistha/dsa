# Missing Number

## 📋 Problem Statement

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

### Examples

**Example 1:**
```
Input: nums = [3,0,1]
Output: 2
```

**Example 2:**
```
Input: nums = [0,1]
Output: 2
```

---

## 💡 Solution: XOR

```python
def missingNumber(nums: list[int]) -> int:
    result = len(nums)
    
    for i, num in enumerate(nums):
        result ^= i ^ num
    
    return result
```

## 💡 Solution: Math (Sum)

```python
def missingNumber(nums: list[int]) -> int:
    n = len(nums)
    expected = n * (n + 1) // 2
    return expected - sum(nums)
```

---

## 🔍 XOR Explanation

```
nums = [3, 0, 1], n = 3

XOR all indices: 0 ^ 1 ^ 2 ^ 3 = ?
XOR all values:  3 ^ 0 ^ 1 = ?
Combined: (0 ^ 3) ^ (1 ^ 0) ^ (2 ^ 1) ^ 3
        = 3 ^ 3 ^ 0 ^ 0 ^ 1 ^ 1 ^ 2
        = 2

All pairs cancel except the missing number!
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **XOR pairs cancel** - a ^ a = 0
2. **Math formula** - Sum of 0 to n
3. **Both O(1) space**
4. **XOR avoids overflow**

---

## 🔗 Related Problems
- Single Number
- Find the Duplicate Number
