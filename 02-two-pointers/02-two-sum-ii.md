# Two Sum II - Input Array Is Sorted

## 📋 Problem Statement

Given a **1-indexed** array of integers `numbers` that is already **sorted in non-decreasing order**, find two numbers such that they add up to a specific `target` number.

Return the indices of the two numbers, `index1` and `index2`, **added by one** as an integer array `[index1, index2]`.

You must use only constant extra space.

### Examples

**Example 1:**
```
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: 2 + 7 = 9. Indices are 1 and 2 (1-indexed).
```

**Example 2:**
```
Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: 2 + 4 = 6.
```

**Example 3:**
```
Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: -1 + 0 = -1.
```

### Constraints
- `2 <= numbers.length <= 3 * 10^4`
- `-1000 <= numbers[i] <= 1000`
- `numbers` is sorted in **non-decreasing order**
- Exactly **one solution** exists
- **Constant extra space** required

---

## 🧠 Thought Process

### Step 1: Understand the Constraints
- Array is SORTED (key insight!)
- Must use O(1) space (no HashMap!)
- 1-indexed output

### Step 2: Why Not HashMap?
- HashMap would work but uses O(n) space
- The sorted property tells us to use TWO POINTERS

### Step 3: Two Pointers Strategy
- Left pointer at start (smallest)
- Right pointer at end (largest)
- Adjust based on sum comparison

```
If sum < target: Need larger sum → move left pointer right
If sum > target: Need smaller sum → move right pointer left
If sum == target: Found it!
```

---

## 💡 Solution

```python
def twoSum(numbers: list[int], target: int) -> list[int]:
    left = 0
    right = len(numbers) - 1
    
    while left < right:
        current_sum = numbers[left] + numbers[right]
        
        if current_sum == target:
            return [left + 1, right + 1]  # 1-indexed
        elif current_sum < target:
            left += 1  # Need larger sum
        else:
            right -= 1  # Need smaller sum
    
    return []  # No solution (shouldn't happen per constraints)
```

---

## 🔍 Detailed Walkthrough

### Example: `numbers = [2, 7, 11, 15], target = 9`

```
Initial:
[2, 7, 11, 15]
 L          R
 
Step 1:
sum = 2 + 15 = 17
17 > 9 → move right pointer left
[2, 7, 11, 15]
 L      R

Step 2:
sum = 2 + 11 = 13
13 > 9 → move right pointer left
[2, 7, 11, 15]
 L  R

Step 3:
sum = 2 + 7 = 9
9 == 9 → Found! Return [1, 2] ✓
```

---

## 📊 Why Two Pointers Work

```
Array: [1, 3, 5, 7, 9], target = 8

Possibilities visualized:
        1   3   5   7   9
    1   2   4   6   8  10
    3   -   6   8  10  12
    5   -   -  10  12  14
    7   -   -   -  14  16
    9   -   -   -   -  18

Starting at corners (1+9=10 > 8):
- Can't use 9 with any number ≤ 1
- Move right pointer: eliminate 9

Now (1+7=8 == 8):
- Found it!
```

**Key insight:** Each step eliminates a row or column of possibilities.

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

- Each step moves one pointer
- Maximum n-1 steps

---

## 🔄 Comparison: Two Pointers vs HashMap

| Aspect | Two Pointers | HashMap |
|--------|--------------|---------|
| Time | O(n) | O(n) |
| Space | O(1) ⭐ | O(n) |
| Requirement | Sorted array | Any array |

**For sorted arrays, Two Pointers is optimal!**

---

## 🎯 Key Takeaways

1. **Sorted array = Think Two Pointers** - Classic pattern!
2. **Move based on comparison** - Sum too big? Move right inward
3. **O(1) space** - No extra data structures needed
4. **1-indexed output** - Don't forget to add 1

---

## ⚠️ Common Mistakes

1. Forgetting 1-indexed output (return `left+1, right+1`)
2. Using HashMap when space must be O(1)
3. Not leveraging sorted property
4. Wrong direction of pointer movement

---

## 🧪 Edge Cases

```python
# All negative
numbers = [-3, -1, 0], target = -4
# -3 + -1 = -4 ✓

# Duplicates
numbers = [2, 2, 3], target = 4
# 2 + 2 = 4 ✓

# Target is sum of extremes
numbers = [1, 5], target = 6
# 1 + 5 = 6 ✓
```

---

## 🔗 Related Problems
- Two Sum (unsorted, use HashMap)
- 3Sum (fix one, Two Pointers for rest)
- 4Sum
- Container With Most Water
