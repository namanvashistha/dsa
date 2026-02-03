# Single Number

## 📋 Problem Statement

Given a **non-empty** array of integers `nums`, every element appears **twice** except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

### Examples

**Example 1:**
```
Input: nums = [2,2,1]
Output: 1
```

**Example 2:**
```
Input: nums = [4,1,2,1,2]
Output: 4
```

---

## 🧠 Thought Process

### Key Insight: XOR Properties
- `a ⊕ a = 0` (same numbers cancel)
- `a ⊕ 0 = a` (identity)
- XOR is commutative and associative

XOR all numbers → pairs cancel, single number remains!

---

## 💡 Solution

```python
def singleNumber(nums: list[int]) -> int:
    result = 0
    for num in nums:
        result ^= num
    return result
```

---

## 🔍 Detailed Walkthrough

```
nums = [4, 1, 2, 1, 2]

result = 0
result = 0 ⊕ 4 = 4
result = 4 ⊕ 1 = 5
result = 5 ⊕ 2 = 7
result = 7 ⊕ 1 = 6  (1 cancels)
result = 6 ⊕ 2 = 4  (2 cancels)

Result: 4 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **XOR cancels pairs** - a ⊕ a = 0
2. **Order doesn't matter** - Commutative
3. **Classic bit manipulation** - Know XOR properties!

---

## 🔗 Related Problems
- Single Number II (appears 3 times)
- Single Number III (two singles)
- Missing Number
