# Coin Change

## 📋 Problem Statement

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount cannot be made up, return `-1`.

You may assume that you have an infinite number of each kind of coin.

### Examples

**Example 1:**
```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

**Example 2:**
```
Input: coins = [2], amount = 3
Output: -1
```

---

## 🧠 Thought Process

### DP Recurrence
```
dp[amount] = min(dp[amount - coin] + 1) for all coins
```

Base case: dp[0] = 0 (0 coins for amount 0)

---

## 💡 Solution

```python
def coinChange(coins: list[int], amount: int) -> int:
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0
    
    for a in range(1, amount + 1):
        for coin in coins:
            if coin <= a:
                dp[a] = min(dp[a], dp[a - coin] + 1)
    
    return dp[amount] if dp[amount] != float('inf') else -1
```

---

## 🔍 Detailed Walkthrough

```
coins = [1, 2, 5], amount = 11

dp = [0, inf, inf, inf, inf, inf, inf, inf, inf, inf, inf, inf]

a=1: dp[1] = min(inf, dp[0]+1) = 1
a=2: dp[2] = min(dp[1]+1, dp[0]+1) = 1
a=3: dp[3] = min(dp[2]+1, dp[1]+1) = 2
...
a=5: dp[5] = min(dp[4]+1, dp[3]+1, dp[0]+1) = 1
...
a=11: dp[11] = min(dp[10]+1, dp[9]+1, dp[6]+1) = 3

Result: 3 (5+5+1) ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(amount × n) |
| Space | O(amount) |

---

## 🎯 Key Takeaways

1. **Classic DP** - Build up from smaller amounts
2. **Try all coins** - Take minimum
3. **Infinity for impossible** - Distinguish from 0
4. **Bottom-up approach** - Avoid recursion overhead

---

## 🔗 Related Problems
- Coin Change II (count ways)
- Perfect Squares
- Minimum Cost For Tickets
