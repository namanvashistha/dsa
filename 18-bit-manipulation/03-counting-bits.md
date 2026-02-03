# Counting Bits

## 📋 Problem Statement

Given an integer `n`, return an array `ans` of length `n + 1` such that for each `i` (0 <= i <= n), `ans[i]` is the number of 1's in the binary representation of `i`.

### Examples

**Example 1:**
```
Input: n = 5
Output: [0,1,1,2,1,2]
Explanation:
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```

---

## 🧠 Thought Process

### Key Insight 💡
**DP with bit manipulation:**
```
i's bits = i's rightmost bit + (i >> 1)'s bits
ans[i] = ans[i >> 1] + (i & 1)
```

Why? Shifting right removes last bit, we add it back with (i & 1).

---

## 💡 Solution

```python
def countBits(n: int) -> list[int]:
    ans = [0] * (n + 1)
    
    for i in range(1, n + 1):
        ans[i] = ans[i >> 1] + (i & 1)
    
    return ans
```

---

## 🔍 Detailed Walkthrough

```
n = 5

i=0: ans[0] = 0 (base)
i=1: ans[1] = ans[0] + 1 = 1
i=2: ans[2] = ans[1] + 0 = 1
i=3: ans[3] = ans[1] + 1 = 2
i=4: ans[4] = ans[2] + 0 = 1
i=5: ans[5] = ans[2] + 1 = 2

Result: [0, 1, 1, 2, 1, 2] ✓
```

---

## 📊 Alternative: i & (i-1)

```python
def countBits(n: int) -> list[int]:
    ans = [0] * (n + 1)
    for i in range(1, n + 1):
        ans[i] = ans[i & (i - 1)] + 1
    return ans
```

`i & (i-1)` removes rightmost 1-bit.

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **DP + bit manipulation** - Use previous results
2. **i >> 1** - Same as i // 2
3. **i & 1** - Get last bit
4. **i & (i-1)** - Remove rightmost 1

---

## 🔗 Related Problems
- Number of 1 Bits
- Reverse Bits
- Power of Two
