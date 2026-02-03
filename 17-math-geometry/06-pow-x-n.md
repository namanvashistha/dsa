# Pow(x, n)

## 📋 Problem Statement

Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., `x^n`).

### Examples

**Example 1:**
```
Input: x = 2.00000, n = 10
Output: 1024.00000
```

**Example 2:**
```
Input: x = 2.00000, n = -2
Output: 0.25000
```

---

## 🧠 Thought Process

### Key Insight 💡
**Binary Exponentiation!**
- x^n = (x²)^(n/2) if n is even
- x^n = x × x^(n-1) if n is odd
- O(log n) instead of O(n)

---

## 💡 Solution: Iterative

```python
def myPow(x: float, n: int) -> float:
    if n < 0:
        x = 1 / x
        n = -n
    
    result = 1
    
    while n:
        if n & 1:
            result *= x
        x *= x
        n >>= 1
    
    return result
```

## 💡 Solution: Recursive

```python
def myPow(x: float, n: int) -> float:
    if n == 0:
        return 1
    if n < 0:
        return 1 / myPow(x, -n)
    if n % 2:
        return x * myPow(x, n - 1)
    return myPow(x * x, n // 2)
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(log n) |
| Space | O(1) iterative / O(log n) recursive |

---

## 🎯 Key Takeaways

1. **Binary exponentiation** - Fast power
2. **Handle negative n** - Reciprocal
3. **Bit operations** - n & 1 for odd check
4. **Square and multiply** - Core technique

---

## 🔗 Related Problems
- Sqrt(x)
- Super Pow
