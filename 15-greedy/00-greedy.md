# 💰 Greedy - NeetCode 150

> 8 problems | Master greedy choice property and local optimum

---

## 1️⃣ Maximum Subarray ⭐⭐ Medium
**The Trick:** Kadane's algorithm - reset when negative
- Track current sum and max sum
- If current < 0, reset to 0
- Update max at each step
- **Remember:** Drop negative prefix, keep if positive

```python
max_sum = float('-inf')
current = 0
for num in nums:
    current = max(num, current + num)  # Start fresh or continue
    max_sum = max(max_sum, current)
```

---

## 2️⃣ Jump Game ⭐⭐ Medium
**The Trick:** Track farthest reachable position
- For each position, update farthest reach
- If current > farthest, unreachable
- **Remember:** Greedily track max reachable

---

## 3️⃣ Jump Game II ⭐⭐ Medium
**The Trick:** Greedy BFS-like approach
- Track current jump's range and next jump's range
- Increment jumps when current range ends
- **Remember:** Count level transitions (BFS idea)

---

## 4️⃣ Gas Station ⭐⭐ Medium
**The Trick:** Start from where surplus begins
- If total gas < total cost → impossible
- Track current surplus, reset start when negative
- **Remember:** Start from first positive surplus point

---

## 5️⃣ Hand of Straights ⭐⭐ Medium
**The Trick:** Sort and greedily form groups
- Count frequencies
- Start from smallest, form consecutive groups
- If can't form group → impossible
- **Remember:** Always start with smallest available

---

## 6️⃣ Merge Intervals ⭐⭐ Medium
**The Trick:** Sort by start, merge overlapping
- Sort intervals by start time
- If current overlaps with last → merge
- Else → add as new interval
- **Remember:** Sort first, then merge adjacent

---

## 7️⃣ Insert Interval ⭐⭐ Medium
**The Trick:** Three phases - before, merge, after
- Add all intervals before new interval
- Merge all overlapping intervals with new
- Add all intervals after
- **Remember:** Before, merge, after

---

## 8️⃣ Non-overlapping Intervals ⭐⭐ Medium
**The Trick:** Sort by end time, greedy selection
- Sort by end time
- Keep interval with earliest end
- Remove overlapping intervals
- **Remember:** Keep shortest ending interval

---

## 🎯 Pattern Recognition

**Greedy Problems Characteristics:**
- Making locally optimal choice
- Choice doesn't depend on future
- Can prove greedy works (exchange argument)

**When to use Greedy:**
- Optimization problem (min/max)
- Can make choice without knowing future
- Local optimum leads to global optimum
- Sorting helps make greedy decision

**Common Greedy Patterns:**

1. **Interval Problems:**
   - Sort by start or end time
   - Greedily select non-overlapping
   - Merge overlapping

2. **Array Traversal:**
   - Make decision at each step
   - Track running state
   - Don't look back

3. **Selection Problems:**
   - Sort by some criteria
   - Greedily pick best choice

**Greedy vs DP:**
- **Greedy:** Make choice once, don't reconsider
- **DP:** Consider all choices, optimal substructure

**How to prove Greedy works:**
1. **Exchange argument:** Show swapping choice doesn't improve
2. **Stay ahead:** Show greedy always ahead or equal to optimal
3. **Structural:** Prove optimal solution has greedy choice property

**Template:**
```python
# 1. Sort (if needed)
items.sort(key=lambda x: x.some_property)

# 2. Initialize tracking variables
result = 0
state = initial_state

# 3. Iterate and make greedy choice
for item in items:
    if greedy_condition(item, state):
        # Make greedy choice
        result += item.value
        state = update(state, item)

return result
```

**Interval Problems Template:**
```python
# Sort intervals
intervals.sort()

merged = []
for interval in intervals:
    if not merged or merged[-1][1] < interval[0]:
        # No overlap
        merged.append(interval)
    else:
        # Overlap, merge
        merged[-1][1] = max(merged[-1][1], interval[1])
```

**Common Greedy Strategies:**

1. **Sort + Scan:**
   - Sort by some property
   - Scan once making decisions

2. **Keep Track of Boundary:**
   - Track current valid range
   - Update as you go

3. **Always Pick Extreme:**
   - Smallest, largest, earliest, latest
   - Depending on problem

**Time Complexity:**
- Usually O(n log n) due to sorting
- Then O(n) scan
- Total: O(n log n)

**Common Mistakes:**
- Assuming greedy works without proof
- Wrong sorting criteria
- Not considering edge cases
- Forgetting to sort first
- Making decision based on future (not greedy!)

**Red Flags (might not be greedy):**
- Need to consider multiple future states
- Optimal substructure requires trying all choices
- Can construct counter-example to greedy

**Key Insights:**
- **Greedy = make best choice now, never look back**
- Sort often reveals greedy strategy
- Interval problems: sort by start or end
- If stuck, try DP - greedy might not work
- Kadane's algorithm = greedy for max subarray
- For intervals: earliest end time usually best

**Pattern Recognition:**
- "Maximum/minimum" + simple constraints → try greedy
- Intervals + overlapping → sort and scan
- Array + running sum/state → greedy scan
- "Can we reach X" + movement → greedy max reach

**When Greedy Fails:**
- Need exact count of ways → DP
- Multiple interdependent choices → DP
- Future choice affects past optimality → DP
- Example: 0/1 Knapsack (greedy fails, need DP)

**Quick Test:**
- Can you make a choice now that's definitely in optimal solution?
- Does sorting help identify that choice?
- If yes to both → probably greedy!
