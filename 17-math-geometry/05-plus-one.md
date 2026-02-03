# Plus One

## 📋 Problem Statement

You are given a large integer represented as an integer array `digits`, where each `digits[i]` is the `ith` digit of the integer. The digits are ordered from most significant to least significant.

Increment the large integer by one and return the resulting array of digits.

### Examples

**Example 1:**
```
Input: digits = [1,2,3]
Output: [1,2,4]
```

**Example 2:**
```
Input: digits = [9,9,9]
Output: [1,0,0,0]
```

---

## 💡 Solution

```python
def plusOne(digits: list[int]) -> list[int]:
    for i in range(len(digits) - 1, -1, -1):
        if digits[i] < 9:
            digits[i] += 1
            return digits
        digits[i] = 0
    
    return [1] + digits
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) or O(n) |

---

## 🎯 Key Takeaways

1. **Start from end** - Least significant digit
2. **Return early** - No carry means done
3. **Set to 0 on carry** - Continue propagating
4. **All 9s case** - Prepend 1

---

## 🔗 Related Problems
- Add Binary
- Add to Array-Form of Integer
