# Minimum Window Substring

## 📋 Problem Statement

Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

### Examples

**Example 1:**
```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: "BANC" is the smallest window that contains 'A', 'B', 'C'.
```

**Example 2:**
```
Input: s = "a", t = "a"
Output: "a"
```

**Example 3:**
```
Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be in the window.
```

### Constraints
- `m == s.length`
- `n == t.length`
- `1 <= m, n <= 10^5`
- `s` and `t` consist of uppercase and lowercase English letters

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Find smallest substring of s containing ALL characters of t
- Characters can appear in any order
- Must include duplicates (if t has "aa", need two 'a's)

### Step 2: Key Insight 💡
Use **variable-size sliding window**:
1. **Expand** right until window contains all chars of t
2. **Shrink** left to find minimum while still valid
3. Record minimum window found
4. Continue expanding and shrinking

### Step 3: Tracking Validity
- Count characters needed from t
- Track how many unique characters are "satisfied" (count met)
- Window valid when all characters satisfied

---

## 💡 Solution

```python
from collections import Counter

def minWindow(s: str, t: str) -> str:
    if not t or not s:
        return ""
    
    # Count characters needed from t
    t_count = Counter(t)
    required = len(t_count)  # Unique chars to match
    
    # Window state
    window_count = {}
    formed = 0  # Unique chars with required frequency
    
    # Result: (window length, left, right)
    result = (float('inf'), 0, 0)
    
    left = 0
    
    for right in range(len(s)):
        # Add right character to window
        char = s[right]
        window_count[char] = window_count.get(char, 0) + 1
        
        # Check if this character's requirement is now satisfied
        if char in t_count and window_count[char] == t_count[char]:
            formed += 1
        
        # Try to shrink window while it's valid
        while formed == required:
            # Update result if current window is smaller
            if right - left + 1 < result[0]:
                result = (right - left + 1, left, right)
            
            # Remove left character from window
            left_char = s[left]
            window_count[left_char] -= 1
            
            # Check if removing breaks the requirement
            if left_char in t_count and window_count[left_char] < t_count[left_char]:
                formed -= 1
            
            left += 1
    
    # Return result
    return "" if result[0] == float('inf') else s[result[1]:result[2] + 1]
```

---

## 🔍 Detailed Walkthrough

### Example: `s = "ADOBECODEBANC", t = "ABC"`

```
t_count = {'A': 1, 'B': 1, 'C': 1}
required = 3

Expand phase:
right=0, char='A':
  window = {'A': 1}, formed = 1 (A satisfied)
  
right=1, char='D':
  window = {'A': 1, 'D': 1}, formed = 1

right=2, char='O':
  window = {'A': 1, 'D': 1, 'O': 1}, formed = 1

right=3, char='B':
  window = {'A': 1, 'D': 1, 'O': 1, 'B': 1}, formed = 2 (B satisfied)

right=4, char='E':
  window = {..., 'E': 1}, formed = 2

right=5, char='C':
  window = {..., 'C': 1}, formed = 3 ✓ ALL SATISFIED!

Shrink phase (formed == 3):
  Window: "ADOBEC" (length 6), save as result
  Remove 'A': window = {'A': 0, ...}, formed = 2 ✗
  left = 1

Expand again:
right=6, char='O':
  formed = 2

right=7, char='D':
  formed = 2

right=8, char='E':
  formed = 2

right=9, char='B':
  formed = 2 (already had B)

right=10, char='A':
  window = {'A': 1, ...}, formed = 3 ✓

Shrink phase:
  Window: "DOBECODEBA" → shrink
  Remove 'D', 'O', 'B', 'E', 'C', 'O', 'D', 'E'...
  Eventually: "BANC" (length 4) is smallest!

Result: "BANC" ✓
```

---

## 📊 Visual Representation

```
s = "ADOBECODEBANC"
t = "ABC"

Step 1: Expand until valid
[A D O B E C] O D E B A N C    valid! length=6
 L         R

Step 2: Shrink until invalid
A [D O B E C] O D E B A N C    invalid (no A)
   L       R

Step 3: Expand again
A D O B E C O D E [B A N C]    valid! length=4 ⭐
                   L     R

No more to expand, result = "BANC"
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m + n) |
| Space | O(m + n) |

Where m = len(s), n = len(t)

**Why O(m)?** Each character is visited at most twice (once by right, once by left).

---

## 🎯 Key Takeaways

1. **Variable sliding window** - Expand, then shrink
2. **Track "formed" count** - Unique chars with satisfied frequency
3. **Shrink while valid** - Find minimum in this phase
4. **Use Counter for frequency matching** - Handle duplicates properly

---

## ⚠️ Common Mistakes

1. Not handling duplicates in t (e.g., t = "AA")
2. Only shrinking once instead of while valid
3. Wrong comparison (== vs >=) for formed count
4. Forgetting to check if left_char is in t_count

---

## 🔄 Template: Minimum Window Pattern

```python
def minWindow(s, condition):
    left = 0
    min_len = float('inf')
    result = ""
    
    for right in range(len(s)):
        # Expand: add s[right] to window
        
        # Shrink: while window is valid
        while is_valid(window):
            # Update result if smaller
            if right - left + 1 < min_len:
                min_len = right - left + 1
                result = s[left:right+1]
            
            # Remove s[left] from window
            left += 1
    
    return result
```

---

## 🔗 Related Problems
- Longest Substring Without Repeating Characters
- Substring with Concatenation of All Words
- Minimum Size Subarray Sum
- Sliding Window Maximum
