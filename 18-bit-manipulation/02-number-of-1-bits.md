# Number of 1 Bits

## 📋 Problem Statement

Write a function that takes the binary representation of an unsigned integer and returns the number of '1' bits it has (also known as the Hamming weight).

### Examples

**Example 1:**
```
Input: n = 00000000000000000000000000001011
Output: 3
```

---

## 💡 Solution: Bit Manipulation

```python
def hammingWeight(n: int) -> int:
    count = 0
    while n:
        count += n & 1
        n >>= 1
    return count
```

## 💡 Solution: Brian Kernighan's

```python
def hammingWeight(n: int) -> int:
    count = 0
    while n:
        n &= (n - 1)  # Remove rightmost 1 bit
        count += 1
    return count
```

---

## 🔍 Brian Kernighan's Explained

```
n = 12 = 1100
n - 1 = 11 = 1011
n & (n-1) = 1000  (count = 1)

n = 8 = 1000
n - 1 = 7 = 0111
n & (n-1) = 0    (count = 2)

Result: 2 bits
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Basic | O(32) | O(1) |
| Brian K. | O(k) | O(1) |

Where k = number of 1 bits

---

## 🎯 Key Takeaways

1. **n & 1** - Check last bit
2. **n & (n-1)** - Remove rightmost 1 bit
3. **Brian Kernighan's** - Only loops k times
4. **Foundation for bit manipulation**

---

## 🔗 Related Problems
- Counting Bits
- Reverse Bits
