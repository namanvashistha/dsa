# Group Anagrams

## 📋 Problem Statement

Given an array of strings `strs`, group the anagrams together. You can return the answer in any order.

An **anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, using all the original letters exactly once.

### Examples

**Example 1:**
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

**Example 2:**
```
Input: strs = [""]
Output: [[""]]
```

**Example 3:**
```
Input: strs = ["a"]
Output: [["a"]]
```

### Constraints
- `1 <= strs.length <= 10^4`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lowercase English letters

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Group strings that are anagrams of each other
- "eat", "tea", "ate" → all anagrams → same group
- Need to identify which strings are anagrams

### Step 2: Key Insight 💡
How do we know two strings are anagrams?
1. **Same sorted version:** "eat" → "aet", "tea" → "aet"
2. **Same character counts:** Both have {a:1, e:1, t:1}

### Step 3: The Approach
Use the **sorted string as a key** in a HashMap:
- All anagrams will have the SAME sorted key
- Group words by their sorted key

```
"eat" → sorted → "aet" (key)
"tea" → sorted → "aet" (same key!)
"tan" → sorted → "ant" (different key)
```

---

## 💡 Solution Approaches

### Approach 1: Sorted String as Key

```python
from collections import defaultdict

def groupAnagrams(strs: list[str]) -> list[list[str]]:
    groups = defaultdict(list)
    
    for word in strs:
        key = ''.join(sorted(word))
        groups[key].append(word)
    
    return list(groups.values())
```

**Walkthrough with Example:** `strs = ["eat","tea","tan","ate","nat","bat"]`
```
word="eat" → key="aet" → groups={"aet": ["eat"]}
word="tea" → key="aet" → groups={"aet": ["eat","tea"]}
word="tan" → key="ant" → groups={"aet": ["eat","tea"], "ant": ["tan"]}
word="ate" → key="aet" → groups={"aet": ["eat","tea","ate"], "ant": ["tan"]}
word="nat" → key="ant" → groups={"aet": ["eat","tea","ate"], "ant": ["tan","nat"]}
word="bat" → key="abt" → groups={..., "abt": ["bat"]}

Result: [["eat","tea","ate"], ["tan","nat"], ["bat"]]
```

### Approach 2: Character Count as Key (Optimal)

```python
from collections import defaultdict

def groupAnagrams(strs: list[str]) -> list[list[str]]:
    groups = defaultdict(list)
    
    for word in strs:
        # Create count array for 26 letters
        count = [0] * 26
        for char in word:
            count[ord(char) - ord('a')] += 1
        
        # Convert to tuple (hashable) for dict key
        key = tuple(count)
        groups[key].append(word)
    
    return list(groups.values())
```

**Why tuple?**
- Lists are not hashable (can't be dict keys)
- Tuples are hashable
- `(3, 0, 0, ..., 1, ..., 1)` represents "aaa...e...t"

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Sorted Key | O(n × k log k) | O(n × k) |
| Count Key | O(n × k) | O(n × k) |

Where:
- `n` = number of strings
- `k` = maximum length of a string

**Why Count Key is faster:**
- Sorting takes O(k log k) per word
- Counting takes O(k) per word
- But constant factor for count array (26 elements) matters

---

## 🔍 Detailed Trace

```python
strs = ["eat", "tea", "tan"]
groups = {}

# Process "eat"
count = [0]*26
count[4] = 1  # 'e' is 4th letter (0-indexed)
count[0] = 1  # 'a' is 0th letter
count[19] = 1 # 't' is 19th letter
key = (1,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0)
groups[key] = ["eat"]

# Process "tea"
count = [0]*26
count[19] = 1 # 't'
count[4] = 1  # 'e'
count[0] = 1  # 'a'
key = (1,0,0,0,1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,0)
# Same key! 
groups[key] = ["eat", "tea"]

# Process "tan"
count = [0]*26
count[19] = 1 # 't'
count[0] = 1  # 'a'
count[13] = 1 # 'n'
key = (1,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,0,0,1,0,0,0,0,0,0)
# Different key!
groups[key] = ["tan"]
```

---

## 🎯 Key Takeaways

1. **Use signature/canonical form for grouping** - Sort or count gives unique identifier
2. **HashMap for grouping** - Key = identifier, Value = list of items
3. **defaultdict simplifies code** - No need to check if key exists
4. **Tuples are hashable, lists are not** - Use tuple for dict keys

---

## ⚠️ Common Mistakes

1. Using list as dictionary key (unhashable)
2. Forgetting to handle empty strings
3. Not converting defaultdict values to list at end

---

## 🔗 Related Problems
- Valid Anagram (check if two strings are anagrams)
- Find All Anagrams in a String (sliding window + anagram check)
- Minimum Number of Steps to Make Two Strings Anagram
