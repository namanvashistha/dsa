# Koko Eating Bananas

## 📋 Problem Statement

Koko loves to eat bananas. There are `n` piles of bananas, the `i`th pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile and eats `k` bananas from it. If the pile has less than `k` bananas, she eats all of them and won't eat any more during that hour.

Return the minimum integer `k` such that she can eat all the bananas within `h` hours.

### Examples

**Example 1:**
```
Input: piles = [3,6,7,11], h = 8
Output: 4
```

**Example 2:**
```
Input: piles = [30,11,23,4,20], h = 5
Output: 30
```

### Constraints
- `1 <= piles.length <= 10^4`
- `piles.length <= h <= 10^9`
- `1 <= piles[i] <= 10^9`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Find minimum eating speed k
- Must finish all piles in h hours
- Each pile takes ceil(pile / k) hours

### Step 2: Key Insight 💡
**Binary Search on the Answer!**
- Speed range: 1 to max(piles)
- For each speed, check if can finish in h hours
- Find minimum valid speed

### Step 3: Check Function
```python
def canFinish(piles, k, h):
    hours = sum(ceil(pile / k) for pile in piles)
    return hours <= h
```

---

## 💡 Solution

```python
import math

def minEatingSpeed(piles: list[int], h: int) -> int:
    def canFinish(k):
        hours = sum(math.ceil(pile / k) for pile in piles)
        return hours <= h
    
    left = 1
    right = max(piles)
    
    while left < right:
        mid = (left + right) // 2
        
        if canFinish(mid):
            right = mid  # Try smaller speed
        else:
            left = mid + 1  # Need faster speed
    
    return left
```

---

## 🔍 Detailed Walkthrough

### Example: `piles = [3, 6, 7, 11], h = 8`

```
Speed range: [1, 11]

k=6: ceil(3/6) + ceil(6/6) + ceil(7/6) + ceil(11/6)
     = 1 + 1 + 2 + 2 = 6 ≤ 8 ✓

k=3: ceil(3/3) + ceil(6/3) + ceil(7/3) + ceil(11/3)
     = 1 + 2 + 3 + 4 = 10 > 8 ✗

Binary search finds k=4:
     = 1 + 2 + 2 + 3 = 8 ≤ 8 ✓

Result: 4 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n log m) |
| Space | O(1) |

Where n = number of piles, m = max(piles)

---

## 🎯 Key Takeaways

1. **Binary Search on Answer** - When searching for optimal value
2. **left < right pattern** - For finding minimum valid
3. **Ceiling division** - ceil(a/b) = (a + b - 1) // b
4. **Monotonic property** - If speed k works, k+1 also works

---

## 🔗 Related Problems
- Capacity To Ship Packages Within D Days
- Split Array Largest Sum
- Minimum Speed to Arrive on Time
