# Best Time to Buy and Sell Stock

## 📋 Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `i`th day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return `0`.

### Examples

**Example 1:**
```
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6).
Profit = 6 - 1 = 5.
```

**Example 2:**
```
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: No profitable transaction possible (prices only go down).
```

### Constraints
- `1 <= prices.length <= 10^5`
- `0 <= prices[i] <= 10^4`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Buy BEFORE sell (can't time travel!)
- Only ONE transaction allowed
- Find maximum profit possible

### Step 2: Brute Force
```python
# For each day, check profit with all future days - O(n²)
max_profit = 0
for buy in range(len(prices)):
    for sell in range(buy + 1, len(prices)):
        profit = prices[sell] - prices[buy]
        max_profit = max(max_profit, profit)
```

### Step 3: Key Insight 💡
For each day as SELL day:
- Best profit = current price - minimum price seen so far
- Track minimum price as we iterate

**One Pass:** Keep track of minimum price and maximum profit simultaneously.

---

## 💡 Solution Approaches

### Approach 1: Track Minimum Price (Optimal)

```python
def maxProfit(prices: list[int]) -> int:
    min_price = float('inf')
    max_profit = 0
    
    for price in prices:
        # Update minimum price seen so far
        min_price = min(min_price, price)
        
        # Calculate profit if we sell today
        profit = price - min_price
        
        # Update maximum profit
        max_profit = max(max_profit, profit)
    
    return max_profit
```

### Approach 2: Two Pointers / Sliding Window

```python
def maxProfit(prices: list[int]) -> int:
    left = 0  # Buy pointer
    right = 1  # Sell pointer
    max_profit = 0
    
    while right < len(prices):
        if prices[left] < prices[right]:
            # Profitable transaction
            profit = prices[right] - prices[left]
            max_profit = max(max_profit, profit)
        else:
            # Found a lower buy price, update left
            left = right
        
        right += 1
    
    return max_profit
```

---

## 🔍 Detailed Walkthrough

### Example: `prices = [7, 1, 5, 3, 6, 4]`

**Approach 1 (Track Minimum):**
```
Day 0: price=7
  min_price = min(inf, 7) = 7
  profit = 7 - 7 = 0
  max_profit = 0

Day 1: price=1
  min_price = min(7, 1) = 1
  profit = 1 - 1 = 0
  max_profit = 0

Day 2: price=5
  min_price = min(1, 5) = 1
  profit = 5 - 1 = 4
  max_profit = 4

Day 3: price=3
  min_price = min(1, 3) = 1
  profit = 3 - 1 = 2
  max_profit = 4

Day 4: price=6
  min_price = min(1, 6) = 1
  profit = 6 - 1 = 5
  max_profit = 5 ⭐

Day 5: price=4
  min_price = min(1, 4) = 1
  profit = 4 - 1 = 3
  max_profit = 5

Result: 5 ✓
```

---

## 📊 Visual Representation

```
Price
  7 │ ●
  6 │         ●
  5 │     ●
  4 │             ●
  3 │       ●
  2 │
  1 │   ●←buy here
  0 └─────────────────
      0 1 2 3 4 5  Day
          sell→↑

Buy at day 1 (price=1), sell at day 4 (price=6)
Profit = 6 - 1 = 5
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | O(n²) | O(1) |
| Track Minimum | O(n) | O(1) |
| Two Pointers | O(n) | O(1) |

---

## 🎯 Key Takeaways

1. **Track minimum seen so far** - For best buy price
2. **Calculate profit at each point** - Could be best sell day
3. **One pass is enough** - Don't need to look back
4. **Greedy approach** - Always buy at minimum, check profit at current

---

## ⚠️ Common Mistakes

1. Not handling empty or single-element arrays
2. Forgetting that buy must come BEFORE sell
3. Returning negative profit instead of 0
4. Over-complicating with nested loops

---

## 🔄 Kadane's Algorithm Perspective

This problem can be viewed as a variant of maximum subarray (Kadane's):
- Convert to difference array: `diff[i] = prices[i] - prices[i-1]`
- Find maximum subarray sum = maximum profit

```python
def maxProfit(prices: list[int]) -> int:
    max_profit = 0
    current_profit = 0
    
    for i in range(1, len(prices)):
        # Add today's gain/loss
        current_profit += prices[i] - prices[i - 1]
        
        # Reset if negative (start fresh)
        current_profit = max(0, current_profit)
        
        # Track maximum
        max_profit = max(max_profit, current_profit)
    
    return max_profit
```

---

## 🔗 Related Problems
- Best Time to Buy and Sell Stock II (multiple transactions)
- Best Time to Buy and Sell Stock III (at most 2 transactions)
- Best Time to Buy and Sell Stock IV (at most k transactions)
- Best Time to Buy and Sell Stock with Cooldown
