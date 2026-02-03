# Valid Anagram

## 📋 Problem Statement

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

### Examples

**Example 1:**
```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Example 2:**
```
Input: s = "rat", t = "car"
Output: false
```

### Constraints
- `1 <= s.length, t.length <= 5 * 10^4`
- `s` and `t` consist of lowercase English letters

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Anagram = same characters, same frequency, different order
- "listen" and "silent" are anagrams
- Both strings must use ALL letters exactly once

### Step 2: Key Observations
1. If lengths differ → cannot be anagrams
2. Both strings must have SAME character frequencies
3. Order doesn't matter, only counts

### Step 3: Consider Approaches
1. **Sorting:** If sorted versions are equal → anagram
2. **HashMap/Counter:** Count characters in both, compare
3. **Single Counter:** Count up for s, count down for t

---

## 💡 Solution Approaches

### Approach 1: Sorting (Simple)

```python
def isAnagram(s: str, t: str) -> bool:
    return sorted(s) == sorted(t)
```

**How it works:**
- Sorting arranges characters in same order
- "anagram" → "aaagmnr"
- "nagaram" → "aaagmnr"
- Same! → True

### Approach 2: HashMap Counter (Optimal)

```python
def isAnagram(s: str, t: str) -> bool:
    if len(s) != len(t):
        return False
    
    count_s = {}
    count_t = {}
    
    for char in s:
        count_s[char] = count_s.get(char, 0) + 1
    
    for char in t:
        count_t[char] = count_t.get(char, 0) + 1
    
    return count_s == count_t
```

**Walkthrough with Example:** `s = "anagram", t = "nagaram"`
```
count_s = {'a': 3, 'n': 1, 'g': 1, 'r': 1, 'm': 1}
count_t = {'n': 1, 'a': 3, 'g': 1, 'r': 1, 'm': 1}
count_s == count_t → True ✓
```

### Approach 3: Using Counter (Pythonic)

```python
from collections import Counter

def isAnagram(s: str, t: str) -> bool:
    return Counter(s) == Counter(t)
```

### Approach 4: Single HashMap (Space Optimized)

```python
def isAnagram(s: str, t: str) -> bool:
    if len(s) != len(t):
        return False
    
    count = {}
    
    # Count up for s
    for char in s:
        count[char] = count.get(char, 0) + 1
    
    # Count down for t
    for char in t:
        if char not in count:
            return False
        count[char] -= 1
        if count[char] < 0:
            return False
    
    return True
```

### Approach 5: Fixed Array (For lowercase letters only)

```python
def isAnagram(s: str, t: str) -> bool:
    if len(s) != len(t):
        return False
    
    count = [0] * 26  # a-z
    
    for i in range(len(s)):
        count[ord(s[i]) - ord('a')] += 1
        count[ord(t[i]) - ord('a')] -= 1
    
    return all(c == 0 for c in count)
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Sorting | O(n log n) | O(n) |
| Two HashMaps | O(n) | O(n) |
| Counter | O(n) | O(n) |
| Single HashMap | O(n) | O(n) |
| Fixed Array | O(n) | O(1) |

*Fixed array is O(1) space because it's always 26 elements*

---

## 🎯 Key Takeaways

1. **Character frequency = anagram check** - Count chars, compare counts
2. **Sorting works too** - But slower at O(n log n)
3. **Early termination** - Check length first to save time
4. **Fixed array optimization** - When character set is known and small

---

## ⚠️ Common Mistakes

1. Forgetting to check length equality first
2. Not handling empty strings
3. Case sensitivity (problem states lowercase only)

---

## 🔗 Related Problems
- Group Anagrams (grouping by anagram signature)
- Find All Anagrams in a String (sliding window)
- Minimum Number of Steps to Make Two Strings Anagram
