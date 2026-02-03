# Permutation in String

## 📋 Problem Statement

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is a substring of `s2`.

### Examples

**Example 1:**
```
Input: s1 = "ab", s2 = "eidbaooo"
Output: true
Explanation: s2 contains "ba" which is a permutation of "ab".
```

**Example 2:**
```
Input: s1 = "ab", s2 = "eidboaoo"
Output: false
```

### Constraints
- `1 <= s1.length, s2.length <= 10^4`
- `s1` and `s2` consist of lowercase English letters

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Find if ANY permutation of s1 exists as substring in s2
- Permutation = same characters, same frequency, any order
- Substring = contiguous

### Step 2: Key Insight 💡
A permutation of s1 has:
1. Same length as s1
2. Same character frequencies as s1

So we need a **fixed-size sliding window** of length `len(s1)` in s2 that has matching character counts!

### Step 3: Strategy
- Count characters in s1
- Slide window of size len(s1) across s2
- Compare character counts at each position

---

## 💡 Solution Approaches

### Approach 1: Compare Counts (Simple)

```python
from collections import Counter

def checkInclusion(s1: str, s2: str) -> bool:
    if len(s1) > len(s2):
        return False
    
    s1_count = Counter(s1)
    window_size = len(s1)
    
    for i in range(len(s2) - window_size + 1):
        window = s2[i:i + window_size]
        if Counter(window) == s1_count:
            return True
    
    return False
```

**Note:** This is O(26 * n) due to Counter creation at each step.

### Approach 2: Sliding Window with Frequency Match (Optimal)

```python
from collections import Counter

def checkInclusion(s1: str, s2: str) -> bool:
    if len(s1) > len(s2):
        return False
    
    s1_count = Counter(s1)
    window_count = Counter()
    
    for i in range(len(s2)):
        # Add right character to window
        window_count[s2[i]] += 1
        
        # Remove leftmost character if window exceeds s1 length
        if i >= len(s1):
            left_char = s2[i - len(s1)]
            window_count[left_char] -= 1
            if window_count[left_char] == 0:
                del window_count[left_char]
        
        # Check if window matches s1
        if window_count == s1_count:
            return True
    
    return False
```

### Approach 3: Using Matches Counter (Most Efficient)

```python
def checkInclusion(s1: str, s2: str) -> bool:
    if len(s1) > len(s2):
        return False
    
    s1_count = [0] * 26
    s2_count = [0] * 26
    
    # Initialize counts for s1 and first window
    for i in range(len(s1)):
        s1_count[ord(s1[i]) - ord('a')] += 1
        s2_count[ord(s2[i]) - ord('a')] += 1
    
    # Count matches (characters with same frequency)
    matches = sum(1 for i in range(26) if s1_count[i] == s2_count[i])
    
    # Slide window
    for i in range(len(s1), len(s2)):
        if matches == 26:
            return True
        
        # Add right character
        idx = ord(s2[i]) - ord('a')
        s2_count[idx] += 1
        if s2_count[idx] == s1_count[idx]:
            matches += 1
        elif s2_count[idx] == s1_count[idx] + 1:
            matches -= 1
        
        # Remove left character
        idx = ord(s2[i - len(s1)]) - ord('a')
        s2_count[idx] -= 1
        if s2_count[idx] == s1_count[idx]:
            matches += 1
        elif s2_count[idx] == s1_count[idx] - 1:
            matches -= 1
    
    return matches == 26
```

---

## 🔍 Detailed Walkthrough

### Example: `s1 = "ab", s2 = "eidbaooo"`

```
s1_count = {'a': 1, 'b': 1}
window_size = 2

Window at i=0: "ei"
  window_count = {'e': 1, 'i': 1}
  ≠ s1_count ✗

Window at i=1: "id"
  window_count = {'i': 1, 'd': 1}
  ≠ s1_count ✗

Window at i=2: "db"
  window_count = {'d': 1, 'b': 1}
  ≠ s1_count ✗

Window at i=3: "ba"
  window_count = {'b': 1, 'a': 1}
  == s1_count ✓

Found permutation at index 3: "ba"
Return True ✓
```

---

## 📊 Visual Representation

```
s1 = "ab"
s2 = "eidbaooo"

Sliding fixed window (size 2):

[e i] d b a o o o   ✗ "ei" ≠ perm("ab")
 e [i d] b a o o o   ✗ "id" ≠ perm("ab")
 e i [d b] a o o o   ✗ "db" ≠ perm("ab")
 e i d [b a] o o o   ✓ "ba" = perm("ab")! 

Found it! Return True
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Compare Counts | O(26 * n) | O(26) |
| Sliding Window | O(n) | O(26) |
| Matches Counter | O(n) | O(26) |

Where n = len(s2)

---

## 🎯 Key Takeaways

1. **Fixed-size sliding window** - Window size = len(s1)
2. **Permutation = same character counts** - No need to generate permutations
3. **Efficient comparison** - Track matches incrementally
4. **Array vs HashMap** - Array of 26 is faster for lowercase letters

---

## ⚠️ Common Mistakes

1. Generating all permutations (too slow!)
2. Not handling case when s1 longer than s2
3. Off-by-one in window boundaries
4. Forgetting to clean up zero counts in Counter

---

## 🔄 Template: Fixed-Size Sliding Window

```python
def fixedSlidingWindow(s, k):
    # k = window size
    for i in range(len(s)):
        # Add s[i] to window
        
        # Remove s[i-k] if window full
        if i >= k:
            # Remove leftmost element
        
        # Check condition when window is full
        if i >= k - 1:
            # Process complete window
```

---

## 🔗 Related Problems
- Find All Anagrams in a String (find ALL positions)
- Minimum Window Substring (variable size window)
- Sliding Window Maximum
- Valid Anagram
