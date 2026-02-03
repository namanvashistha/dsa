# Design Add and Search Words Data Structure

## 📋 Problem Statement

Design a data structure that supports adding new words and finding if a string matches any previously added string.

`WordDictionary()` Initializes the object.
`void addWord(word)` Adds word to the data structure.
`bool search(word)` Returns true if there is any string that matches word. word may contain dots `.` where dots can match any letter.

### Examples

```
Input: ["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
       [[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
Output: [null,null,null,null,false,true,true,true]
```

---

## 🧠 Thought Process

### Key Insight 💡
- Use **Trie** for storage
- For `.`, try all children (DFS)
- For regular char, follow the path

---

## 💡 Solution

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class WordDictionary:
    def __init__(self):
        self.root = TrieNode()
    
    def addWord(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word: str) -> bool:
        def dfs(node, i):
            if i == len(word):
                return node.is_end
            
            char = word[i]
            
            if char == '.':
                # Try all children
                for child in node.children.values():
                    if dfs(child, i + 1):
                        return True
                return False
            else:
                if char not in node.children:
                    return False
                return dfs(node.children[char], i + 1)
        
        return dfs(self.root, 0)
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| addWord | O(m) | O(m) |
| search | O(26^m) worst | O(m) |

Where m = word length

---

## 🎯 Key Takeaways

1. **Trie + DFS** - For wildcard matching
2. **`.` means try all** - Explore all children
3. **Regular char** - Follow single path
4. **Check is_end** - Complete word match

---

## 🔗 Related Problems
- Implement Trie
- Word Search II
