# Encode and Decode Strings

## 📋 Problem Statement

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Implement the `encode` and `decode` methods.

### Examples

**Example 1:**
```
Input: ["leet","code","love","you"]
Output: ["leet","code","love","you"]
Explanation: 
  encode → "4#leet4#code4#love3#you"
  decode → ["leet","code","love","you"]
```

**Example 2:**
```
Input: ["we","say",":","yes"]
Output: ["we","say",":","yes"]
```

### Constraints
- `0 <= strs.length < 100`
- `0 <= strs[i].length < 200`
- `strs[i]` contains any possible characters including special characters

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Convert list of strings to single string (encode)
- Convert back to original list (decode)
- Must handle ANY characters (including delimiters!)

### Step 2: Why Simple Delimiter Fails
```
❌ Using comma: ["a,b", "c"] → "a,b,c" → ["a", "b", "c"] WRONG!
❌ Using |: ["a|b", "c"] → "a|b|c" → ["a", "b", "c"] WRONG!
```

Any delimiter can appear in the strings themselves!

### Step 3: Key Insight 💡
Use **length prefix** encoding:
- Store the LENGTH of each string BEFORE the string
- Use a separator that won't be confused with the length

Format: `length#string`

```
["hello"] → "5#hello"
["ab", "cdef"] → "2#ab4#cdef"
```

### Step 4: Why This Works
- Numbers tell us exactly how many characters to read
- '#' separates length from content
- Even if string contains "5#", we know to read exactly 5 chars after '#'

---

## 💡 Solution

```python
class Codec:
    def encode(self, strs: list[str]) -> str:
        """Encodes a list of strings to a single string."""
        encoded = ""
        for s in strs:
            encoded += str(len(s)) + "#" + s
        return encoded
    
    def decode(self, s: str) -> list[str]:
        """Decodes a single string to a list of strings."""
        result = []
        i = 0
        
        while i < len(s):
            # Find the '#' to get the length
            j = i
            while s[j] != '#':
                j += 1
            
            # Extract length
            length = int(s[i:j])
            
            # Extract the string (starts after '#', has 'length' characters)
            start = j + 1
            end = start + length
            result.append(s[start:end])
            
            # Move to next encoded string
            i = end
        
        return result
```

---

## 🔍 Detailed Walkthrough

### Encoding: `["leet", "code", "love", "you"]`

```
s = "leet"  → len=4  → "4#leet"
s = "code"  → len=4  → "4#code"
s = "love"  → len=4  → "4#love"
s = "you"   → len=3  → "3#you"

Result: "4#leet4#code4#love3#you"
```

### Decoding: `"4#leet4#code4#love3#you"`

```
i=0: Find '#' at j=1
     length = int("4") = 4
     string = s[2:6] = "leet"
     result = ["leet"]
     i = 6

i=6: Find '#' at j=7
     length = int("4") = 4
     string = s[8:12] = "code"
     result = ["leet", "code"]
     i = 12

i=12: Find '#' at j=13
      length = int("4") = 4
      string = s[14:18] = "love"
      result = ["leet", "code", "love"]
      i = 18

i=18: Find '#' at j=19
      length = int("3") = 3
      string = s[20:23] = "you"
      result = ["leet", "code", "love", "you"]
      i = 23

i=23 >= len(s)=23, exit loop

Result: ["leet", "code", "love", "you"] ✓
```

### Edge Case: String contains "#" and numbers

```
Input: ["5#abc"]
Encode: "5#5#abc"
        ↑
        length=5, then read exactly 5 chars: "5#abc" ✓

Decode:
i=0: Find '#' at j=1
     length = 5
     string = s[2:7] = "5#abc" ✓
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| Encode | O(n) | O(n) |
| Decode | O(n) | O(n) |

Where n = total number of characters across all strings

---

## 🎯 Key Takeaways

1. **Length prefix encoding** - Reliable way to encode variable-length data
2. **Avoid delimiter-only approaches** - Delimiters can appear in content
3. **Know the exact length** - Allows correct parsing regardless of content
4. **Common serialization technique** - Used in network protocols

---

## ⚠️ Common Mistakes

1. Using a simple delimiter that could appear in strings
2. Not handling empty strings correctly
3. Off-by-one errors in string slicing
4. Forgetting to convert length to string/int

---

## 🔄 Alternative Approaches

### Escaping Special Characters
```python
# Less elegant but works
def encode(strs):
    return '\\,'.join(s.replace('\\', '\\\\').replace(',', '\\,') for s in strs)

def decode(s):
    # Complex parsing needed to handle escaped characters
    pass
```

### Using Non-printable Characters
```python
# Use ASCII 0 as delimiter (rarely in strings)
def encode(strs):
    return chr(0).join(strs)

def decode(s):
    return s.split(chr(0))
```

The length-prefix approach is most robust and commonly used.

---

## 🌐 Real-World Applications

This encoding pattern is used in:
- **Network protocols** (length-prefixed messages)
- **File formats** (binary data serialization)
- **Database storage** (variable-length fields)
- **Redis protocol** (RESP format)

---

## 🔗 Related Problems
- Serialize and Deserialize Binary Tree
- String Compression
- Design TinyURL
