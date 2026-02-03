# Valid Palindrome

## 📋 Problem Statement

A phrase is a **palindrome** if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

### Examples

**Example 1:**
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Example 2:**
```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

**Example 3:**
```
Input: s = " "
Output: true
Explanation: After removing non-alphanumeric, it's empty string "".
```

### Constraints
- `1 <= s.length <= 2 * 10^5`
- `s` consists only of printable ASCII characters

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Ignore case (convert to lowercase)
- Ignore non-alphanumeric characters (spaces, punctuation)
- Check if remaining string is palindrome

### Step 2: Approach Options
1. **Clean then check:** Remove non-alphanumeric, then compare with reverse
2. **Two pointers:** Compare from both ends, skip non-alphanumeric

### Step 3: Two Pointers is Better
- No extra string creation
- O(1) space instead of O(n)
- Single pass comparison

---

## 💡 Solution Approaches

### Approach 1: Clean and Compare (Simple)

```python
def isPalindrome(s: str) -> bool:
    # Remove non-alphanumeric and convert to lowercase
    cleaned = ''.join(char.lower() for char in s if char.isalnum())
    
    # Compare with reverse
    return cleaned == cleaned[::-1]
```

### Approach 2: Two Pointers (Optimal)

```python
def isPalindrome(s: str) -> bool:
    left = 0
    right = len(s) - 1
    
    while left < right:
        # Skip non-alphanumeric from left
        while left < right and not s[left].isalnum():
            left += 1
        
        # Skip non-alphanumeric from right
        while left < right and not s[right].isalnum():
            right -= 1
        
        # Compare characters (case-insensitive)
        if s[left].lower() != s[right].lower():
            return False
        
        left += 1
        right -= 1
    
    return True
```

---

## 🔍 Detailed Walkthrough

### Example: `s = "A man, a plan, a canal: Panama"`

```
Initial: left=0 ('A'), right=29 ('a')

Step 1:
  s[0]='A' is alphanumeric ✓
  s[29]='a' is alphanumeric ✓
  'a' == 'a' ✓
  left=1, right=28

Step 2:
  s[1]=' ' NOT alphanumeric → left=2
  s[2]='m' is alphanumeric ✓
  s[28]='m' is alphanumeric ✓
  'm' == 'm' ✓
  left=3, right=27

Step 3:
  s[3]='a' is alphanumeric ✓
  s[27]='a' is alphanumeric ✓
  'a' == 'a' ✓
  left=4, right=26

... continue comparing ...

Eventually left >= right → return True ✓
```

---

## 📊 Visual Representation

```
Original: "A man, a plan, a canal: Panama"

Two pointers approach:
  ↓                              ↓
  A man, a plan, a canal: Panama
  L                              R

After skipping and comparing:
     ↓                        ↓
  A man, a plan, a canal: Panama
     L                        R

... pointers move toward center ...

When L >= R, we're done!
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Clean and Compare | O(n) | O(n) |
| Two Pointers | O(n) | O(1) |

---

## 🎯 Key Takeaways

1. **Two pointers from both ends** - Classic palindrome check pattern
2. **Skip invalid characters** - Move pointers when non-alphanumeric
3. **Case-insensitive comparison** - Use `.lower()` before comparing
4. **Check `left < right`** - Avoid infinite loop

---

## ⚠️ Common Mistakes

1. Forgetting to skip non-alphanumeric in BOTH directions
2. Not handling case sensitivity
3. Missing the `left < right` check in inner while loops
4. Confusing `isalnum()` with `isalpha()` (alnum includes digits)

---

## 🔧 Helper Functions

```python
# Check if character is alphanumeric
char.isalnum()  # Returns True for a-z, A-Z, 0-9

# Convert to lowercase
char.lower()

# Manual alphanumeric check (alternative)
def is_alphanumeric(c):
    return (
        ('a' <= c <= 'z') or
        ('A' <= c <= 'Z') or
        ('0' <= c <= '9')
    )
```

---

## 🔗 Related Problems
- Valid Palindrome II (can remove one character)
- Palindrome Linked List (check in linked list)
- Longest Palindromic Substring
- Palindrome Number
