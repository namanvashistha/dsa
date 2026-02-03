# Hand of Straights

## 📋 Problem Statement

Alice has some number of cards, and wants to arrange them into groups so that each group is of size `groupSize`, and consists of `groupSize` consecutive cards.

Given an integer array `hand` where `hand[i]` is the value written on the `ith` card and an integer `groupSize`, return `true` if she can rearrange the cards, or `false` otherwise.

### Examples

**Example 1:**
```
Input: hand = [1,2,3,6,2,3,4,7,8], groupSize = 3
Output: true
Explanation: [1,2,3], [2,3,4], [6,7,8]
```

---

## 💡 Solution

```python
from collections import Counter

def isNStraightHand(hand: list[int], groupSize: int) -> bool:
    if len(hand) % groupSize:
        return False
    
    count = Counter(hand)
    
    for card in sorted(count.keys()):
        if count[card] > 0:
            num_groups = count[card]
            
            # Try to form groups starting from this card
            for i in range(groupSize):
                if count[card + i] < num_groups:
                    return False
                count[card + i] -= num_groups
    
    return True
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n log n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Greedy from smallest** - Start groups from minimum
2. **Count frequency** - Track available cards
3. **Check consecutive** - Need groupSize consecutive cards
4. **Length divisibility** - Quick check first

---

## 🔗 Related Problems
- Divide Array in Sets of K Consecutive Numbers
- Split Array into Consecutive Subsequences
