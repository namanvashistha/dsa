# Gas Station

## 📋 Problem Statement

There are `n` gas stations along a circular route. You are given two integer arrays:
- `gas[i]` - amount of gas at station `i`
- `cost[i]` - cost to travel from station `i` to `i+1`

Return the starting gas station's index if you can travel around the circuit once clockwise, otherwise return `-1`.

### Examples

**Example 1:**
```
Input: gas = [1,2,3,4,5], cost = [3,4,5,1,2]
Output: 3
```

---

## 🧠 Thought Process

### Key Insights 💡
1. If total gas >= total cost, solution exists
2. If we can't reach station j from i, any station between i and j also can't reach j
3. Start from the station after the "valley"

---

## 💡 Solution

```python
def canCompleteCircuit(gas: list[int], cost: list[int]) -> int:
    if sum(gas) < sum(cost):
        return -1
    
    tank = 0
    start = 0
    
    for i in range(len(gas)):
        tank += gas[i] - cost[i]
        
        if tank < 0:
            start = i + 1
            tank = 0
    
    return start
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Total check first** - Determine if solution exists
2. **Reset on failure** - Start fresh from next station
3. **Single pass** - O(n) solution
4. **Greedy skip** - Skip all failed starting points

---

## 🔗 Related Problems
- Minimum Fuel Cost to Report to Capital
