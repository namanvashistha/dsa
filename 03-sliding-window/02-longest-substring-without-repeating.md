# Longest Substring Without Repeating Characters

## 📋 Problem Statement

Given a string `s`, find the length of the **longest substring** without repeating characters.

### Examples

**Example 1:**
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with length 3.
```

**Example 2:**
```
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with length 1.
```

**Example 3:**
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with length 3.
Note: "pwke" is a subsequence, not a substring.
```

### Constraints
- `0 <= s.length <= 5 * 10^4`
- `s` consists of English letters, digits, symbols, and spaces

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Find longest SUBSTRING (contiguous!)
- No repeating characters in the substring
- Return LENGTH, not the substring itself

### Step 2: Key Insight 💡
Use **sliding window**:
- Expand right to include new characters
- When duplicate found, shrink from left until no duplicate
- Track maximum window size

### Step 3: Data Structure
Use **HashSet** to track characters in current window:
- O(1) to check if character exists
- O(1) to add/remove

---

## 💡 Solution Approaches

### Approach 1: Sliding Window with HashSet

```python
def lengthOfLongestSubstring(s: str) -> int:
    char_set = set()
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Shrink window while duplicate exists
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        
        # Add current character
        char_set.add(s[right])
        
        # Update maximum length
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

### Approach 2: Sliding Window with HashMap (Jump Optimization)

```python
def lengthOfLongestSubstring(s: str) -> int:
    char_index = {}  # Character -> its last index
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        char = s[right]
        
        # If character seen and within current window, jump left
        if char in char_index and char_index[char] >= left:
            left = char_index[char] + 1
        
        # Update character's index
        char_index[char] = right
        
        # Update maximum length
        max_length = max(max_length, right - left + 1)
    
    return max_length
```

---

## 🔍 Detailed Walkthrough (HashSet Approach)

### Example: `s = "abcabcbb"`

```
Initial: char_set={}, left=0, max_length=0

right=0, char='a':
  'a' not in set
  char_set = {'a'}
  window = "a", length = 1
  max_length = 1

right=1, char='b':
  'b' not in set
  char_set = {'a', 'b'}
  window = "ab", length = 2
  max_length = 2

right=2, char='c':
  'c' not in set
  char_set = {'a', 'b', 'c'}
  window = "abc", length = 3
  max_length = 3

right=3, char='a':
  'a' IS in set! → shrink
    remove 'a', left = 1
  char_set = {'b', 'c'}
  Now 'a' not in set, add it
  char_set = {'a', 'b', 'c'}
  window = "bca", length = 3
  max_length = 3

right=4, char='b':
  'b' IS in set! → shrink
    remove 'b', left = 2
  char_set = {'a', 'c'}
  Now 'b' not in set, add it
  char_set = {'a', 'b', 'c'}
  window = "cab", length = 3
  max_length = 3

... continue ...

Result: 3 ✓
```

---

## 📊 Visual Representation

```
s = "abcabcbb"

Step 1: [a] b c a b c b b     window="a", len=1
         L
         R

Step 2: [a b] c a b c b b     window="ab", len=2
         L R

Step 3: [a b c] a b c b b     window="abc", len=3 ⭐
         L   R

Step 4: a [b c a] b c b b     window="bca", len=3
           L   R
         ↑ moved left past 'a'

Step 5: a b [c a b] c b b     window="cab", len=3
             L   R

... window slides right ...
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| HashSet | O(n) | O(min(m, n))* |
| HashMap (Jump) | O(n) | O(min(m, n)) |

*m = size of character set (e.g., 26 for lowercase letters)*

**Why O(n) for HashSet approach?**
- Each character is added at most once
- Each character is removed at most once
- Total operations: 2n = O(n)

---

## 🎯 Key Takeaways

1. **Sliding window for substring problems** - Classic pattern!
2. **HashSet for uniqueness check** - O(1) lookup
3. **Shrink from left when constraint violated** - Remove until valid
4. **HashMap for jump optimization** - Skip directly to valid position

---

## ⚠️ Common Mistakes

1. Using subsequence logic instead of substring
2. Not removing characters when shrinking window
3. Off-by-one errors in window length calculation
4. Forgetting to update max_length after each valid window

---

## 🔄 Template: Variable Sliding Window

```python
def slidingWindow(s):
    window = {}  # or set
    left = 0
    result = 0
    
    for right in range(len(s)):
        # Expand: add s[right] to window
        
        # Shrink: while window is invalid
        while not_valid(window):
            # Remove s[left] from window
            left += 1
        
        # Update result
        result = max(result, right - left + 1)
    
    return result
```

---

## 🔗 Related Problems
- Longest Repeating Character Replacement
- Minimum Window Substring
- Substring with Concatenation of All Words
- Longest Substring with At Most Two Distinct Characters
