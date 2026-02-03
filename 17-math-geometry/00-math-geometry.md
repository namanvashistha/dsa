# 🔢 Math & Geometry - NeetCode 150

> 8 problems | Master mathematical patterns and geometric algorithms

---

## 1️⃣ Rotate Image ⭐⭐ Medium
**The Trick:** Transpose then reverse each row
- Step 1: Transpose (swap `[i][j]` with `[j][i]`)
- Step 2: Reverse each row
- **Alternative:** Rotate in groups of 4
- **Remember:** Transpose + reverse = 90° clockwise

---

## 2️⃣ Spiral Matrix ⭐⭐ Medium
**The Trick:** Four boundaries, shrink inward
- Track top, bottom, left, right boundaries
- Go right → down → left → up
- Shrink boundary after each direction
- **Remember:** Four directions, update boundaries

---

## 3️⃣ Set Matrix Zeroes ⭐⭐ Medium
**The Trick:** Use first row/col as markers
- Use first row and column to mark zeros
- Extra variables for first row/col themselves
- Set zeros based on markers
- **Remember:** First row/col = marker space

---

## 4️⃣ Happy Number ⭐ Easy
**The Trick:** Detect cycle with set or fast/slow
- Calculate sum of squares of digits
- If reaches 1 → happy
- If cycle detected → not happy
- **Remember:** Cycle detection problem

---

## 5️⃣ Plus One ⭐ Easy
**The Trick:** Handle carry digit by digit
- Start from rightmost digit
- Add 1, handle carry
- If all 9's, prepend 1
- **Remember:** Carry propagation

---

## 6️⃣ Pow(x, n) ⭐⭐ Medium
**The Trick:** Fast exponentiation (binary)
- If n even: `x^n = (x^(n/2))^2`
- If n odd: `x^n = x × x^(n-1)`
- Handle negative n: `x^(-n) = 1 / x^n`
- **Remember:** Divide and conquer, O(log n)

```python
def myPow(x, n):
    if n == 0:
        return 1
    if n < 0:
        x = 1 / x
        n = -n
    
    result = 1
    while n > 0:
        if n % 2 == 1:
            result *= x
        x *= x
        n //= 2
    return result
```

---

## 7️⃣ Multiply Strings ⭐⭐ Medium
**The Trick:** Grade school multiplication
- Multiply digit by digit
- Store results in array (position based)
- Handle carry at end
- `num1[i] × num2[j]` → result at `[i+j]` and `[i+j+1]`
- **Remember:** Position mapping in result array

---

## 8️⃣ Detect Squares ⭐⭐ Medium
**The Trick:** Count points, check diagonals
- Store point frequencies in HashMap
- For each point pair (diagonal), check other corners
- Count = product of frequencies
- **Remember:** Fix diagonal, check if other 2 corners exist

---

## 🎯 Pattern Recognition

**Math Problems Categories:**

1. **Matrix Manipulation:**
   - Rotate, transpose, spiral
   - In-place vs extra space
   
2. **Number Operations:**
   - Large numbers as strings/arrays
   - Digit manipulation
   - Binary representation

3. **Geometric:**
   - Points, lines, shapes
   - Distance, area calculations

4. **Mathematical Algorithms:**
   - GCD, LCM
   - Prime numbers
   - Fast exponentiation
   - Modular arithmetic

**Common Techniques:**

### 1. Matrix Rotation (90° clockwise)
```python
# Transpose
for i in range(n):
    for j in range(i, n):
        matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

# Reverse each row
for row in matrix:
    row.reverse()
```

### 2. Spiral Traversal
```python
top, bottom, left, right = 0, m-1, 0, n-1

while top <= bottom and left <= right:
    # Right
    for j in range(left, right+1):
        result.append(matrix[top][j])
    top += 1
    
    # Down
    for i in range(top, bottom+1):
        result.append(matrix[i][right])
    right -= 1
    
    # Left (if still valid)
    if top <= bottom:
        for j in range(right, left-1, -1):
            result.append(matrix[bottom][j])
        bottom -= 1
    
    # Up (if still valid)
    if left <= right:
        for i in range(bottom, top-1, -1):
            result.append(matrix[i][left])
        left += 1
```

### 3. Fast Exponentiation
```python
def power(x, n):
    result = 1
    while n > 0:
        if n % 2 == 1:  # Odd power
            result *= x
        x *= x  # Square base
        n //= 2  # Halve power
    return result
```

### 4. GCD (Euclidean Algorithm)
```python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a
```

### 5. Prime Sieve (Eratosthenes)
```python
def sieve(n):
    prime = [True] * (n+1)
    prime[0] = prime[1] = False
    
    for i in range(2, int(n**0.5) + 1):
        if prime[i]:
            for j in range(i*i, n+1, i):
                prime[j] = False
    
    return [i for i in range(n+1) if prime[i]]
```

**Geometry Formulas:**

- **Distance:** `sqrt((x2-x1)² + (y2-y1)²)`
- **Manhattan Distance:** `|x2-x1| + |y2-y1|`
- **Slope:** `(y2-y1) / (x2-x1)`
- **Midpoint:** `((x1+x2)/2, (y1+y2)/2)`
- **Area of Triangle:** `|x1(y2-y3) + x2(y3-y1) + x3(y1-y2)| / 2`

**Bit Manipulation Shortcuts:**
- `x & 1`: check if odd
- `x >> 1`: divide by 2
- `x << 1`: multiply by 2
- `x & (x-1)`: remove rightmost 1
- `x & -x`: get rightmost 1

**Modular Arithmetic:**
- `(a + b) % m = ((a % m) + (b % m)) % m`
- `(a × b) % m = ((a % m) × (b % m)) % m`
- `(a - b) % m = ((a % m) - (b % m) + m) % m`

**Time Complexity:**
- Fast exponentiation: O(log n)
- GCD: O(log min(a, b))
- Prime sieve: O(n log log n)
- Matrix operations: O(n²) or O(n³)

**Common Mistakes:**
- Integer overflow in multiplication
- Off-by-one in spiral/matrix problems
- Not handling negative numbers
- Forgetting edge cases (0, 1, negative)
- Float precision issues
- Matrix boundary conditions

**Key Insights:**
- **Matrix rotation:** Transpose + reverse
- **Spiral:** Track 4 boundaries, shrink inward
- **Large numbers:** Use string/array digit by digit
- **Fast power:** Binary exponentiation O(log n)
- **Geometry:** Often use HashMap to count points
- **In-place matrix:** Use first row/col as markers

**Optimization Techniques:**
- Binary representation for powers
- Memoization for recursive math
- Early termination in loops
- Avoid floating point when possible

**Edge Cases:**
- Empty matrix
- 1×1 matrix
- Very large numbers
- Negative numbers
- Zero cases
- Overflow/underflow

**Pattern Recognition:**
- Matrix manipulation → in-place with markers
- Large numbers → string/array representation
- Power/exponentiation → binary method
- Geometric → HashMap for counting
- Cycle detection → fast/slow or set
- Spiral/zigzag → boundary tracking

**When Stuck:**
- Draw small example (3×3 matrix)
- Work through manually
- Look for mathematical property
- Consider binary representation
- Think about invariants
