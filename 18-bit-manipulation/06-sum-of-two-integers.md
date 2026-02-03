# Sum of Two Integers

## 📋 Problem Statement

Given two integers `a` and `b`, return the sum of the two integers without using the operators `+` and `-`.

### Examples

**Example 1:**
```
Input: a = 1, b = 2
Output: 3
```

**Example 2:**
```
Input: a = 2, b = 3
Output: 5
```

---

## 🧠 Thought Process

### Key Insight 💡
Use bit manipulation:
- **XOR (^):** Sum without carry
- **AND (&) << 1:** Carry bits

Repeat until no carry.

```
a = 2: 010
b = 3: 011

XOR:   001 (sum without carry)
AND:   010 → 100 (carry shifted left)

Next:
a = 1: 001
b = 4: 100

XOR:   101 (5)
AND:   000

No carry → done! Result: 5
```

---

## 💡 Solution

```python
def getSum(a: int, b: int) -> int:
    # Mask for 32-bit integer
    MASK = 0xFFFFFFFF
    MAX_INT = 0x7FFFFFFF
    
    while b != 0:
        carry = (a & b) << 1
        a = (a ^ b) & MASK
        b = carry & MASK
    
    # Handle negative numbers
    return a if a <= MAX_INT else ~(a ^ MASK)
```

---

## 📊 Why Mask in Python?

Python integers have infinite precision. We need to simulate 32-bit overflow:
- MASK = 0xFFFFFFFF (32 ones)
- MAX_INT = 0x7FFFFFFF (max positive 32-bit)

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(1) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **XOR = sum without carry** - 1+1=0 (no carry in result)
2. **AND << 1 = carry** - Carry to next position
3. **Loop until no carry** - Then done
4. **Python needs masking** - Infinite precision

---

## 🔗 Related Problems
- Add Binary
- Multiply Strings (without *)
- Divide Two Integers (without /)
