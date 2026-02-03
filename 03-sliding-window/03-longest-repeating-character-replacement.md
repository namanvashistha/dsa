# Longest Repeating Character Replacement

## 📋 Problem Statement

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return the length of the longest substring containing the same letter you can get after performing the above operations.

### Examples

**Example 1:**
```
Input: s = "ABAB", k = 2
Output: 4
Explanation: Replace the two 'A's with 'B's or vice versa.
```

**Example 2:**
```
Input: s = "AABABBA", k = 1
Output: 4
Explanation: Replace 'B' at index 3 with 'A'. Result is "AAAABBA".
The substring "AAAA" has length 4.
```

### Constraints
- `1 <= s.length <= 10^5`
- `s` consists of only uppercase English letters
- `0 <= k <= s.length`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Replace at most k characters
- Make substring with all same characters
- Find longest such substring

### Step 2: Key Insight 💡
For a window to be valid:
```
(window size) - (count of most frequent char) ≤ k
```

**Why?** 
- If most frequent char appears `maxCount` times in window
- We need to replace `windowSize - maxCount` other characters
- If this is ≤ k, we can make all characters the same!

### Step 3: Sliding Window Strategy
- Expand right to include new character
- If window becomes invalid, shrink from left
- Track character frequencies and max frequency

---

## 💡 Solution

```python
def characterReplacement(s: str, k: int) -> int:
    count = {}  # Character frequencies in current window
    max_count = 0  # Max frequency of any char in window
    max_length = 0
    left = 0
    
    for right in range(len(s)):
        # Add right character to window
        char = s[right]
        count[char] = count.get(char, 0) + 1
        
        # Update max frequency
        max_count = max(max_count, count[char])
        
        # Window size = right - left + 1
        # Characters to replace = window_size - max_count
        # If > k, shrink window
        while (right - left + 1) - max_count > k:
            count[s[left]] -= 1
            left += 1
        
        # Update maximum valid window length
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

---

## 🔍 Detailed Walkthrough

### Example: `s = "AABABBA", k = 1`

```
Initial: count={}, max_count=0, left=0, max_length=0

right=0, char='A':
  count = {'A': 1}
  max_count = 1
  window_size = 1, to_replace = 1 - 1 = 0 ≤ 1 ✓
  max_length = 1

right=1, char='A':
  count = {'A': 2}
  max_count = 2
  window_size = 2, to_replace = 2 - 2 = 0 ≤ 1 ✓
  max_length = 2

right=2, char='B':
  count = {'A': 2, 'B': 1}
  max_count = 2
  window_size = 3, to_replace = 3 - 2 = 1 ≤ 1 ✓
  max_length = 3

right=3, char='A':
  count = {'A': 3, 'B': 1}
  max_count = 3
  window_size = 4, to_replace = 4 - 3 = 1 ≤ 1 ✓
  max_length = 4 ⭐

right=4, char='B':
  count = {'A': 3, 'B': 2}
  max_count = 3
  window_size = 5, to_replace = 5 - 3 = 2 > 1 ✗
  → shrink: remove s[0]='A', left=1
  count = {'A': 2, 'B': 2}
  window_size = 4, to_replace = 4 - 3 = 1 ≤ 1 ✓
  max_length = 4

right=5, char='B':
  count = {'A': 2, 'B': 3}
  max_count = 3
  window_size = 5, to_replace = 5 - 3 = 2 > 1 ✗
  → shrink: remove s[1]='A', left=2
  count = {'A': 1, 'B': 3}
  window_size = 4, to_replace = 4 - 3 = 1 ≤ 1 ✓
  max_length = 4

right=6, char='A':
  count = {'A': 2, 'B': 3}
  max_count = 3
  window_size = 5, to_replace = 5 - 3 = 2 > 1 ✗
  → shrink: remove s[2]='B', left=3
  count = {'A': 2, 'B': 2}
  window_size = 4, to_replace = 4 - 3 = 1 ≤ 1 ✓
  max_length = 4

Result: 4 ✓
```

---

## 📊 Visual Representation

```
s = "AABABBA", k = 1

Step 1: [A] A B A B B A       window="A", valid ✓
         L
         R

Step 2: [A A] B A B B A       window="AA", valid ✓
         L R

Step 3: [A A B] A B B A       window="AAB", replace 1 B ✓
         L   R

Step 4: [A A B A] B B A       window="AABA", replace 1 B ✓ ⭐
         L     R

Step 5: A [A B A B] B A       window="ABAB", replace 2 ✗→shrink
           L     R

Step 6: A A [B A B B] A       window="BABB", replace 1 A ✓
             L     R
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(26) = O(1) |

---

## 🔍 Why We Don't Update max_count When Shrinking

**Important optimization:** We don't decrease `max_count` when shrinking.

**Why is this correct?**
- We're looking for the LONGEST valid window
- A window of size L was valid at some point (with that max_count)
- We only need to find windows LONGER than L
- For a longer window, max_count must be higher anyway
- So not decreasing max_count doesn't give wrong answers!

**Example:**
- Found valid window of size 4 with max_count=3
- For size 5 window to be valid: need max_count ≥ 4
- The old max_count=3 will make size 5 invalid, which is correct

---

## 🎯 Key Takeaways

1. **Valid window: windowSize - maxCount ≤ k** - Core condition
2. **Track max frequency** - Determines replacements needed
3. **Don't need to update max_count on shrink** - Optimization
4. **Sliding window pattern** - Expand, check, shrink if invalid

---

## ⚠️ Common Mistakes

1. Trying to track which character to replace (not needed!)
2. Updating max_count when shrinking (unnecessary)
3. Wrong window size calculation
4. Not understanding the validity condition

---

## 🔗 Related Problems
- Longest Substring Without Repeating Characters
- Max Consecutive Ones III (similar replace k pattern)
- Minimum Window Substring
- Permutation in String
