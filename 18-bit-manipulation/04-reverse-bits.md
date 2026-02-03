# Reverse Bits

## 📋 Problem Statement

Reverse bits of a given 32 bits unsigned integer.

### Examples

**Example 1:**
```
Input:  n = 00000010100101000001111010011100
Output:   964176192 (00111001011110000010100101000000)
```

---

## 💡 Solution

```python
def reverseBits(n: int) -> int:
    result = 0
    
    for i in range(32):
        bit = (n >> i) & 1
        result |= bit << (31 - i)
    
    return result
```

## 💡 Solution: Alternative

```python
def reverseBits(n: int) -> int:
    result = 0
    
    for _ in range(32):
        result = (result << 1) | (n & 1)
        n >>= 1
    
    return result
```

---

## 🔍 Walkthrough

```
n = 4 = 100 (binary)

Iteration 0: bit=0, result |= 0 << 31
Iteration 1: bit=0, result |= 0 << 30
Iteration 2: bit=1, result |= 1 << 29

Result has 1 at position 29 from right
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(32) = O(1) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Extract bit** - (n >> i) & 1
2. **Place at reversed position** - bit << (31 - i)
3. **Build result with OR**
4. **Fixed 32 iterations** - Always process all bits

---

## 🔗 Related Problems
- Number of 1 Bits
- Reverse Integer
