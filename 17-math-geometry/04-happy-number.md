# Happy Number

## 📋 Problem Statement

Write an algorithm to determine if a number `n` is happy.

A happy number is defined by:
- Starting with any positive integer, replace the number by the sum of the squares of its digits.
- Repeat until the number equals 1, or it loops endlessly in a cycle.
- Return `true` if 1, `false` otherwise.

### Examples

**Example 1:**
```
Input: n = 19
Output: true
Explanation: 
1² + 9² = 82
8² + 2² = 68
6² + 8² = 100
1² + 0² + 0² = 1
```

---

## 💡 Solution: Floyd's Cycle Detection

```python
def isHappy(n: int) -> bool:
    def get_next(num):
        total = 0
        while num > 0:
            digit = num % 10
            total += digit * digit
            num //= 10
        return total
    
    slow = n
    fast = get_next(n)
    
    while fast != 1 and slow != fast:
        slow = get_next(slow)
        fast = get_next(get_next(fast))
    
    return fast == 1
```

## 💡 Solution: HashSet

```python
def isHappy(n: int) -> bool:
    seen = set()
    
    while n != 1 and n not in seen:
        seen.add(n)
        n = sum(int(d) ** 2 for d in str(n))
    
    return n == 1
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Floyd's | O(log n) | O(1) |
| HashSet | O(log n) | O(log n) |

---

## 🎯 Key Takeaways

1. **Cycle detection** - Will either reach 1 or cycle
2. **Floyd's tortoise and hare** - O(1) space
3. **Sum of digit squares** - Core operation
4. **HashSet alternative** - Simpler but more space

---

## 🔗 Related Problems
- Linked List Cycle
- Add Digits
