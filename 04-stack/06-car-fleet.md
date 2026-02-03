# Car Fleet

## 📋 Problem Statement

There are `n` cars going to the same destination along a one-lane road. The destination is `target` miles away.

You are given two integer arrays `position` and `speed`, both of length `n`, where `position[i]` is the position of the `i`th car and `speed[i]` is the speed.

A car can never pass another car ahead of it, but it can catch up to it and drive bumper to bumper at the same speed. The faster car will slow down to match.

A **car fleet** is some non-empty set of cars driving at the same position and same speed. Return the number of car fleets that will arrive at the destination.

### Examples

**Example 1:**
```
Input: target = 12, position = [10,8,0,5,3], speed = [2,4,1,1,3]
Output: 3
Explanation: 
- Cars at 10 and 8 become a fleet (meet at target)
- Car at 0 arrives alone
- Cars at 5 and 3 become a fleet
```

---

## 🧠 Thought Process

### Key Insight 💡
1. Sort cars by position (descending - closest to target first)
2. Calculate time to reach target for each car
3. If car behind has less time, it catches up → same fleet
4. If car behind has more time, it forms new fleet

Use **monotonic stack** to track fleets.

---

## 💡 Solution

```python
def carFleet(target: int, position: list[int], speed: list[int]) -> int:
    # Pair and sort by position descending
    cars = sorted(zip(position, speed), reverse=True)
    
    stack = []  # Time to reach target
    
    for pos, spd in cars:
        time = (target - pos) / spd
        
        # If this car takes longer, it's a new fleet
        if not stack or time > stack[-1]:
            stack.append(time)
        # Otherwise it catches up to car ahead (same fleet)
    
    return len(stack)
```

---

## 🔍 Detailed Walkthrough

```
target = 12
Sorted by position: [(10,2), (8,4), (5,1), (3,3), (0,1)]

Car at 10: time = (12-10)/2 = 1.0, stack=[1.0]
Car at 8:  time = (12-8)/4 = 1.0, 1.0 <= 1.0 → catches up
           stack=[1.0]
Car at 5:  time = (12-5)/1 = 7.0, 7.0 > 1.0 → new fleet
           stack=[1.0, 7.0]
Car at 3:  time = (12-3)/3 = 3.0, 3.0 <= 7.0 → catches up
           stack=[1.0, 7.0]
Car at 0:  time = (12-0)/1 = 12.0, 12.0 > 7.0 → new fleet
           stack=[1.0, 7.0, 12.0]

Result: 3 fleets ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n log n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Sort by position** - Process from closest to target
2. **Time = distance / speed** - Key metric
3. **Slower car blocks** - Forms new fleet
4. **Stack tracks fleet leaders** - Their arrival times

---

## 🔗 Related Problems
- Car Fleet II
- Asteroid Collision
