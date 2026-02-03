# Find the Duplicate Number

## 📋 Problem Statement

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return this repeated number.

You must solve the problem **without** modifying the array and uses only constant extra space.

### Examples

**Example 1:**
```
Input: nums = [1,3,4,2,2]
Output: 2
```

---

## 🧠 Thought Process

### Key Insight 💡
Treat array as a **linked list**!
- Value at index i points to next index
- Duplicate = cycle in the linked list
- Use **Floyd's Cycle Detection**!

---

## 💡 Solution

```python
def findDuplicate(nums: list[int]) -> int:
    # Phase 1: Find intersection point
    slow = fast = nums[0]
    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break
    
    # Phase 2: Find cycle start
    slow2 = nums[0]
    while slow != slow2:
        slow = nums[slow]
        slow2 = nums[slow2]
    
    return slow
```

---

## 🔍 Detailed Walkthrough

```
nums = [1, 3, 4, 2, 2]
Index:  0  1  2  3  4

Linked list representation:
0 → 1 → 3 → 2 → 4 → 2 (cycle!)
                ↑     |
                ← ← ←

Phase 1: Find meeting point
  slow: 0→1→3→2→4→2
  fast: 0→3→4→2→4→2
  Meet at 2

Phase 2: Find cycle start
  slow: 2→4→2
  slow2: 0→1→3→2
  Meet at 2

Result: 2 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Array as linked list** - Index → Value mapping
2. **Duplicate = cycle** - Two indices point to same value
3. **Floyd's algorithm** - O(1) space cycle detection
4. **Cycle start = duplicate** - Key insight!

---

## 🔗 Related Problems
- Linked List Cycle II
- Missing Number
- Set Mismatch
