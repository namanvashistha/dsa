# Best Time to Buy and Sell Stock with Cooldown

## 📋 Problem Statement

You are given an array `prices` where `prices[i]` is the price of a stock on the `ith` day.

Find the maximum profit. You may complete as many transactions as you like but after you sell, you must wait one day before you can buy again (cooldown).

### Examples

**Example 1:**
```
Input: prices = [1,2,3,0,2]
Output: 3
Explanation: buy, sell, cooldown, buy, sell
```

---

## 🧠 Thought Process

### States:
- **hold**: Have stock
- **sold**: Just sold (in cooldown)
- **rest**: No stock, not in cooldown

---

## 💡 Solution

```python
def maxProfit(prices: list[int]) -> int:
    if not prices:
        return 0
    
    hold = -prices[0]  # Buy on day 0
    sold = 0
    rest = 0
    
    for i in range(1, len(prices)):
        prev_hold = hold
        
        hold = max(hold, rest - prices[i])  # Keep or buy
        rest = max(rest, sold)              # Keep or from sold
        sold = prev_hold + prices[i]        # Sell
    
    return max(sold, rest)
```

---

## 📊 State Transitions

```
         sell
hold  ←------→  sold
  ↑               ↓
  |     buy      rest
  ←----------- 
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Three states** - hold, sold, rest
2. **sold → rest** - Cooldown transition
3. **rest → hold** - Buy after cooldown
4. **Track prev_hold** - Before updating

---

## 🔗 Related Problems
- Best Time to Buy and Sell Stock
- Best Time to Buy and Sell Stock with Transaction Fee
