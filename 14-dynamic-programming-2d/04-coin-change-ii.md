# Coin Change II

## 📋 Problem Statement

You are given an integer array `coins` representing coins of different denominations and an integer `amount`.

Return the number of combinations that make up that amount. If no combination, return `0`.

### Examples

**Example 1:**
```
Input: amount = 5, coins = [1,2,5]
Output: 4
Explanation: 5=5, 5=2+2+1, 5=2+1+1+1, 5=1+1+1+1+1
```

---

## 🧠 Thought Process

### Key Insight 💡
**Unbounded Knapsack** - Can use each coin unlimited times.
- Order coins outer, amount inner (for combinations, not permutations)

---

## 💡 Solution

```python
def change(amount: int, coins: list[int]) -> int:
    dp = [0] * (amount + 1)
    dp[0] = 1  # One way to make 0
    
    for coin in coins:
        for a in range(coin, amount + 1):
            dp[a] += dp[a - coin]
    
    return dp[amount]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(amount × n) |
| Space | O(amount) |

---

## 🎯 Key Takeaways

1. **Coins outer loop** - Counts combinations, not permutations
2. **Forward iteration** - Unbounded usage allowed
3. **dp[0] = 1** - Base case
4. **Different from Coin Change I** - Count vs min coins

---

## 🔗 Related Problems
- Coin Change
- Combination Sum IV
