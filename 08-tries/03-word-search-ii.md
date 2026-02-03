# Word Search II

## 📋 Problem Statement

Given an `m x n` board of characters and a list of strings `words`, return all words found in the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

### Examples

```
Input: board = [["o","a","a","n"],
                ["e","t","a","e"],
                ["i","h","k","r"],
                ["i","f","l","v"]], 
       words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
```

---

## 🧠 Thought Process

### Step 1: Naive Approach
Search each word separately → O(m×n×4^L × W) - Too slow!

### Step 2: Key Insight 💡
**Build Trie from words, then DFS once!**
- Trie enables searching all words simultaneously
- Prune branches not in any word

---

## 💡 Solution

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.word = None

class Solution:
    def findWords(self, board: list[list[str]], words: list[str]) -> list[str]:
        # Build Trie
        root = TrieNode()
        for word in words:
            node = root
            for char in word:
                if char not in node.children:
                    node.children[char] = TrieNode()
                node = node.children[char]
            node.word = word
        
        result = []
        rows, cols = len(board), len(board[0])
        
        def dfs(r, c, node):
            char = board[r][c]
            
            if char not in node.children:
                return
            
            child = node.children[char]
            
            if child.word:
                result.append(child.word)
                child.word = None  # Avoid duplicates
            
            # Mark visited
            board[r][c] = '#'
            
            # Explore neighbors
            for dr, dc in [(0,1), (0,-1), (1,0), (-1,0)]:
                nr, nc = r + dr, c + dc
                if 0 <= nr < rows and 0 <= nc < cols:
                    dfs(nr, nc, child)
            
            # Backtrack
            board[r][c] = char
            
            # Prune empty branches
            if not child.children:
                del node.children[char]
        
        for r in range(rows):
            for c in range(cols):
                dfs(r, c, root)
        
        return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n × 4^L) |
| Space | O(total chars in words) |

Where L = max word length

---

## 🎯 Key Takeaways

1. **Trie + DFS** - Classic combination
2. **Store word at leaf** - Easy retrieval
3. **Prune empty branches** - Optimization
4. **Mark visited in-place** - Use special char

---

## 🔗 Related Problems
- Word Search (single word)
- Implement Trie
- Design Add and Search Words
