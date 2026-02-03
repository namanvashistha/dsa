# Detect Squares

## 📋 Problem Statement

Design a data structure that supports:
- `add(point)`: Adds a new point.
- `count(point)`: Counts the number of ways to choose three points from the data structure such that the three points and the query point form an axis-aligned square with positive area.

### Examples

```
Input: ["DetectSquares", "add", "add", "add", "count", "count", "add", "count"]
       [[], [[3, 10]], [[11, 2]], [[3, 2]], [[11, 10]], [[14, 8]], [[11, 2]], [[11, 10]]]
Output: [null, null, null, null, 1, 0, null, 2]
```

---

## 💡 Solution

```python
from collections import defaultdict

class DetectSquares:
    def __init__(self):
        self.points = defaultdict(int)
        self.x_to_ys = defaultdict(list)
    
    def add(self, point: list[int]) -> None:
        x, y = point
        self.points[(x, y)] += 1
        self.x_to_ys[x].append(y)
    
    def count(self, point: list[int]) -> int:
        x1, y1 = point
        count = 0
        
        # For each point with same x coordinate
        for y2 in self.x_to_ys[x1]:
            if y2 == y1:
                continue
            
            side = abs(y2 - y1)
            
            # Check both directions for the square
            for x2 in [x1 + side, x1 - side]:
                count += (self.points[(x1, y2)] * 
                          self.points[(x2, y1)] * 
                          self.points[(x2, y2)])
        
        return count
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| add | O(1) | O(n) |
| count | O(n) | O(1) |

---

## 🎯 Key Takeaways

1. **Axis-aligned square** - Sides parallel to axes
2. **Find diagonal** - Given two points, find other two
3. **Count duplicates** - Multiply frequencies
4. **Two directions** - Square can be left or right

---

## 🔗 Related Problems
- Valid Square
- Count Squares with Same Color
