# 🔄 Backtracking - NeetCode 150

> 9 problems | Master explore-and-backtrack pattern for all combinations

---

## 1️⃣ Subsets ⭐⭐ Medium
**The Trick:** Include or exclude each element
- For each element: add it OR skip it
- Base case: reached end → add current subset
- Backtrack: remove last added element
- **Remember:** 2^n subsets, explore both choices

---

## 2️⃣ Combination Sum ⭐⭐ Medium
**The Trick:** Try each number, can reuse
- For each candidate: add it, recurse, remove
- Can use same number multiple times
- Track remaining target
- **Remember:** Explore with same index (reuse allowed)

---

## 3️⃣ Permutations ⭐⭐ Medium
**The Trick:** Try each unused element at each position
- For each position, try all unused elements
- Mark as used, recurse, unmark (backtrack)
- Base case: all positions filled
- **Remember:** Track used elements

---

## 4️⃣ Subsets II (with duplicates) ⭐⭐ Medium
**The Trick:** Sort first, skip duplicates
- Sort array to group duplicates
- Skip duplicate: `if i > start and nums[i] == nums[i-1]`
- **Remember:** Sort + skip consecutive duplicates

---

## 5️⃣ Combination Sum II ⭐⭐ Medium
**The Trick:** Can't reuse, skip duplicates
- Sort array first
- Skip duplicates at same level
- Move to next index (no reuse)
- **Remember:** Sort + skip duplicates + i+1 for next

---

## 6️⃣ Word Search ⭐⭐ Medium
**The Trick:** DFS on board with backtracking
- Try all 4 directions from each cell
- Mark visited, recurse, unmark (backtrack)
- Match characters with word
- **Remember:** Mark visited → recurse → unmark

---

## 7️⃣ Palindrome Partitioning ⭐⭐ Medium
**The Trick:** Try all valid palindrome cuts
- For each position, check if prefix is palindrome
- If yes, recurse on remaining suffix
- Backtrack and try next cut
- **Remember:** Check palindrome before recursing

---

## 8️⃣ Letter Combinations of Phone Number ⭐⭐ Medium
**The Trick:** Build combinations digit by digit
- For current digit, try all letters
- Recurse with next digit
- **Remember:** Like nested loops but recursive

---

## 9️⃣ N-Queens ⭐⭐⭐ Hard
**The Trick:** Place queen row by row, check valid
- For each row, try placing in each column
- Check: same column, diagonal, anti-diagonal
- Track invalid columns/diagonals with sets
- **Remember:** Track cols, diags, anti-diags in sets

**Diagonal tracking:**
- Diagonal: `row - col` (constant for same diagonal)
- Anti-diagonal: `row + col` (constant for same anti-diagonal)

---

## 🎯 Pattern Recognition

**Use Backtracking when:**
- Generate all combinations/permutations
- Explore all possible solutions
- Need to try different paths
- Can prune invalid paths early

**Backtracking Template:**
```python
def backtrack(path, choices):
    if is_solution(path):
        result.append(path.copy())  # Must copy!
        return
    
    for choice in choices:
        if is_valid(choice):
            # Make choice
            path.append(choice)
            
            # Recurse
            backtrack(path, new_choices)
            
            # Backtrack (undo choice)
            path.pop()
```

**Key Patterns:**

1. **Subsets/Combinations:** Choose or don't choose
   - Time: O(2^n)
   - Track current subset
   
2. **Permutations:** Try each element at each position
   - Time: O(n!)
   - Track used elements
   
3. **Grid/Board:** DFS with mark/unmark
   - Mark visited → recurse → unmark
   - 4 directions: up, down, left, right

**Avoiding Duplicates:**
```python
# Sort first, then skip same consecutive
nums.sort()
for i in range(start, len(nums)):
    if i > start and nums[i] == nums[i-1]:
        continue  # Skip duplicate at same level
    # Process nums[i]
```

**Common Patterns by Problem:**
- **Subsets:** Include/exclude each element
- **Combinations:** Start index to avoid duplicates
- **Permutations:** Track used array
- **Grid search:** Mark → recurse → unmark
- **Partition:** Try all valid splits

**Time Complexity:**
- Subsets: O(2^n × n) - 2^n subsets, n to copy each
- Permutations: O(n! × n) - n! permutations
- Combinations: O(2^n × n)

**Space Complexity:**
- Recursion depth: O(n)
- Storing results: O(solution_count × solution_size)

**Common Mistakes:**
- Forgetting to copy path when adding to result
- Not backtracking (not removing last choice)
- Not handling duplicates in input
- Infinite recursion (no base case or wrong condition)
- Modifying global state without restoring

**Optimization Techniques:**
- **Pruning:** Stop early if path can't lead to solution
- **Sorting:** Group duplicates for easier skipping
- **Memoization:** If subproblems overlap (DP-like)

**Key Insights:**
- Backtracking = DFS with undo
- Always copy path before adding to result
- Duplicates handling: sort + skip consecutive
- Board problems: mark → recurse → unmark
- Track choices made, explore all possibilities

**Debug Tips:**
- Print current path at each step
- Verify backtracking happens (undo operations)
- Check if copying path (not reference)
- Test with small inputs first
