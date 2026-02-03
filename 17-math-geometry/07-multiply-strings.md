# Multiply Strings

## 📋 Problem Statement

Given two non-negative integers `num1` and `num2` represented as strings, return the product of `num1` and `num2`, also represented as a string.

You must not use any built-in BigInteger library or convert the inputs to integer directly.

### Examples

**Example 1:**
```
Input: num1 = "123", num2 = "456"
Output: "56088"
```

---

## 💡 Solution

```python
def multiply(num1: str, num2: str) -> str:
    if num1 == "0" or num2 == "0":
        return "0"
    
    m, n = len(num1), len(num2)
    result = [0] * (m + n)
    
    for i in range(m - 1, -1, -1):
        for j in range(n - 1, -1, -1):
            mul = int(num1[i]) * int(num2[j])
            p1, p2 = i + j, i + j + 1
            
            total = mul + result[p2]
            result[p2] = total % 10
            result[p1] += total // 10
    
    # Skip leading zeros
    result_str = ''.join(map(str, result))
    return result_str.lstrip('0') or '0'
```

---

## 🔍 Walkthrough

```
num1 = "123", num2 = "45"

Position in result = i + j (for carry) and i + j + 1 (for digit)

    1   2   3
        4   5
    ---------
        1   5  (3×5)
    1   0      (3×4)
        1   0  (2×5)
    0   8      (2×4)
        0   5  (1×5)
    0   4      (1×4)
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m + n) |

---

## 🎯 Key Takeaways

1. **Position formula** - i + j for carry, i + j + 1 for digit
2. **Result array size** - m + n max
3. **Handle zeros** - Edge case
4. **Manual multiplication** - Grade school algorithm

---

## 🔗 Related Problems
- Add Strings
- Add Two Numbers
