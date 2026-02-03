# Valid Sudoku

## 📋 Problem Statement

Determine if a `9 x 9` Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits `1-9` without repetition.
2. Each column must contain the digits `1-9` without repetition.
3. Each of the nine `3 x 3` sub-boxes must contain the digits `1-9` without repetition.

**Note:**
- A Sudoku board could be valid but not necessarily solvable.
- Only the filled cells need to be validated.

### Examples

**Example 1:**
```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

**Example 2:**
```
Input: board = 
[["8","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,...
Output: false
Explanation: Two 8's in first column
```

### Constraints
- `board.length == 9`
- `board[i].length == 9`
- `board[i][j]` is a digit `1-9` or `'.'`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Check validity, NOT solvability
- Three constraints: rows, columns, 3×3 boxes
- Empty cells ('.') are ignored

### Step 2: Key Insight 💡
We need to track seen numbers in:
1. Each of the 9 rows
2. Each of the 9 columns
3. Each of the 9 3×3 boxes

**Use HashSets** to detect duplicates!

### Step 3: Box Indexing
The tricky part is identifying which 3×3 box a cell belongs to.

```
Boxes numbered 0-8:
┌───┬───┬───┐
│ 0 │ 1 │ 2 │
├───┼───┼───┤
│ 3 │ 4 │ 5 │
├───┼───┼───┤
│ 6 │ 7 │ 8 │
└───┴───┴───┘

For cell (row, col):
box_index = (row // 3) * 3 + (col // 3)
```

Examples:
- (0, 0) → box 0: (0//3)*3 + (0//3) = 0
- (1, 4) → box 1: (1//3)*3 + (4//3) = 0 + 1 = 1
- (5, 7) → box 5: (5//3)*3 + (7//3) = 3 + 2 = 5

---

## 💡 Solution Approaches

### Approach 1: Three Sets per Dimension

```python
def isValidSudoku(board: list[list[str]]) -> bool:
    # Initialize sets for each row, column, and box
    rows = [set() for _ in range(9)]
    cols = [set() for _ in range(9)]
    boxes = [set() for _ in range(9)]
    
    for r in range(9):
        for c in range(9):
            num = board[r][c]
            
            if num == '.':
                continue
            
            # Calculate box index
            box_idx = (r // 3) * 3 + (c // 3)
            
            # Check if already seen
            if num in rows[r]:
                return False
            if num in cols[c]:
                return False
            if num in boxes[box_idx]:
                return False
            
            # Add to sets
            rows[r].add(num)
            cols[c].add(num)
            boxes[box_idx].add(num)
    
    return True
```

### Approach 2: Single Set with Encoded Keys

```python
def isValidSudoku(board: list[list[str]]) -> bool:
    seen = set()
    
    for r in range(9):
        for c in range(9):
            num = board[r][c]
            
            if num == '.':
                continue
            
            box_idx = (r // 3) * 3 + (c // 3)
            
            # Create unique identifiers
            row_key = f"row{r}:{num}"
            col_key = f"col{c}:{num}"
            box_key = f"box{box_idx}:{num}"
            
            if row_key in seen or col_key in seen or box_key in seen:
                return False
            
            seen.add(row_key)
            seen.add(col_key)
            seen.add(box_key)
    
    return True
```

### Approach 3: Using DefaultDict

```python
from collections import defaultdict

def isValidSudoku(board: list[list[str]]) -> bool:
    rows = defaultdict(set)
    cols = defaultdict(set)
    boxes = defaultdict(set)
    
    for r in range(9):
        for c in range(9):
            num = board[r][c]
            
            if num == '.':
                continue
            
            box_key = (r // 3, c // 3)
            
            if (num in rows[r] or 
                num in cols[c] or 
                num in boxes[box_key]):
                return False
            
            rows[r].add(num)
            cols[c].add(num)
            boxes[box_key].add(num)
    
    return True
```

---

## 🔍 Detailed Trace

```python
board = [
    ["5","3",".",".","7",".",".",".","."],
    ["6",".",".","1","9","5",".",".","."],
    ...
]

Processing cell (0,0) = "5":
  box_idx = (0//3)*3 + (0//3) = 0
  rows[0] = {"5"}
  cols[0] = {"5"}
  boxes[0] = {"5"}

Processing cell (0,1) = "3":
  box_idx = 0
  rows[0] = {"5", "3"}
  cols[1] = {"3"}
  boxes[0] = {"5", "3"}

Processing cell (0,2) = ".":
  Skip (empty)

...continue for all cells...

No duplicates found → return True
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Three Sets | O(81) = O(1) | O(81) = O(1) |
| Single Set | O(81) = O(1) | O(81×3) = O(1) |

*Technically O(1) since board is always 9×9*

---

## 🎯 Key Takeaways

1. **HashSet for duplicate detection** - Perfect for "no repetition" constraints
2. **Box indexing formula** - `(row // 3) * 3 + (col // 3)` maps cell to box
3. **Check all constraints simultaneously** - One pass through the board
4. **Skip empty cells** - Only validate filled cells

---

## ⚠️ Common Mistakes

1. Not skipping '.' cells
2. Wrong box index calculation
3. Checking row/col/box separately (inefficient)
4. Confusing 0-indexed with 1-indexed

---

## 📐 Visual Box Index Map

```
Cell positions → Box indices:

(0,0)(0,1)(0,2) (0,3)(0,4)(0,5) (0,6)(0,7)(0,8)
(1,0)(1,1)(1,2) (1,3)(1,4)(1,5) (1,6)(1,7)(1,8)
(2,0)(2,1)(2,2) (2,3)(2,4)(2,5) (2,6)(2,7)(2,8)
    BOX 0           BOX 1           BOX 2

(3,0)(3,1)(3,2) (3,3)(3,4)(3,5) (3,6)(3,7)(3,8)
(4,0)(4,1)(4,2) (4,3)(4,4)(4,5) (4,6)(4,7)(4,8)
(5,0)(5,1)(5,2) (5,3)(5,4)(5,5) (5,6)(5,7)(5,8)
    BOX 3           BOX 4           BOX 5

(6,0)(6,1)(6,2) (6,3)(6,4)(6,5) (6,6)(6,7)(6,8)
(7,0)(7,1)(7,2) (7,3)(7,4)(7,5) (7,6)(7,7)(7,8)
(8,0)(8,1)(8,2) (8,3)(8,4)(8,5) (8,6)(8,7)(8,8)
    BOX 6           BOX 7           BOX 8
```

---

## 🔗 Related Problems
- Sudoku Solver (backtracking to solve)
- N-Queens (constraint satisfaction)
- Check If Every Row and Column Contains All Numbers
