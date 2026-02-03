# Reverse Integer

## 📋 Problem Statement

Given a signed 32-bit integer `x`, return `x` with its digits reversed. If reversing `x` causes the value to go outside the signed 32-bit integer range `[-2³¹, 2³¹ - 1]`, then return `0`.

### Examples

**Example 1:**
```
Input: x = 123
Output: 321
```

**Example 2:**
```
Input: x = -123
Output: -321
```

---

## 💡 Solution

```python
def reverse(x: int) -> int:
    INT_MIN, INT_MAX = -2**31, 2**31 - 1
    
    sign = 1 if x >= 0 else -1
    x = abs(x)
    
    result = 0
    while x:
        digit = x % 10
        x //= 10
        
        # Check overflow before multiplying
        if result > (INT_MAX - digit) // 10:
            return 0
        
        result = result * 10 + digit
    
    return sign * result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(log x) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Check overflow before operation** - Not after
2. **Handle sign separately**
3. **Extract digits** - x % 10, x //= 10
4. **32-bit limits** - ±2^31

---

## 🔗 Related Problems
- String to Integer (atoi)
- Reverse Bits
