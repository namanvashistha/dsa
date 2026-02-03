# 🔢 Bit Manipulation - NeetCode 150

> 7 problems | Master bitwise operations and tricks

---

## 1️⃣ Single Number ⭐ Easy
**The Trick:** XOR all numbers
- XOR properties: `a ⊕ a = 0`, `a ⊕ 0 = a`
- All pairs cancel out, single remains
- **Remember:** `result = num1 ⊕ num2 ⊕ num3 ⊕ ...`

---

## 2️⃣ Number of 1 Bits ⭐ Easy
**The Trick:** Count set bits with `n & (n-1)`
- Each `n & (n-1)` removes rightmost 1
- Count how many times until 0
- **Remember:** `n & (n-1)` removes rightmost 1 bit

```python
count = 0
while n:
    n &= n - 1
    count += 1
```

---

## 3️⃣ Counting Bits ⭐ Easy
**The Trick:** DP with `dp[i] = dp[i >> 1] + (i & 1)`
- Number of 1's in i = 1's in i//2 + last bit
- **Remember:** Shift right + check last bit

---

## 4️⃣ Reverse Bits ⭐ Easy
**The Trick:** Build result bit by bit
- Extract LSB of n: `n & 1`
- Add to result: `result = (result << 1) | (n & 1)`
- Shift n right: `n >>= 1`
- **Remember:** Extract, add, shift

---

## 5️⃣ Missing Number ⭐ Easy
**The Trick:** XOR all indices and values
- XOR all numbers 0 to n
- XOR all numbers in array
- Missing number remains
- **Alternative:** Sum formula `n(n+1)/2 - sum(array)`
- **Remember:** XOR cancels pairs

---

## 6️⃣ Sum of Two Integers ⭐⭐ Medium
**The Trick:** XOR for sum, AND for carry
- Sum without carry: `a ⊕ b`
- Carry: `(a & b) << 1`
- Repeat until no carry
- **Remember:** XOR = sum, AND = carry

```python
while b != 0:
    carry = (a & b) << 1
    a = a ^ b
    b = carry
```

---

## 7️⃣ Reverse Integer ⭐⭐ Medium
**The Trick:** Extract digits, build reversed
- Extract: `digit = x % 10`
- Build: `result = result * 10 + digit`
- Handle overflow and negative
- **Remember:** Modulo and divide by 10

---

## 🎯 Bit Manipulation Fundamentals

**Basic Operations:**

| Operation | Symbol | Example | Result |
|-----------|--------|---------|--------|
| AND | `&` | `5 & 3` | `1` (0101 & 0011 = 0001) |
| OR | `\|` | `5 \| 3` | `7` (0101 \| 0011 = 0111) |
| XOR | `^` | `5 ^ 3` | `6` (0101 ^ 0011 = 0110) |
| NOT | `~` | `~5` | `-6` (flip all bits) |
| Left Shift | `<<` | `5 << 1` | `10` (multiply by 2) |
| Right Shift | `>>` | `5 >> 1` | `2` (divide by 2) |

**XOR Properties:**
- `a ^ 0 = a` (identity)
- `a ^ a = 0` (self-inverse)
- `a ^ b ^ a = b` (commutative, cancels)
- Useful for finding unique elements

**Common Bit Tricks:**

```python
# Check if kth bit is set
def is_set(n, k):
    return (n >> k) & 1

# Set kth bit
def set_bit(n, k):
    return n | (1 << k)

# Clear kth bit
def clear_bit(n, k):
    return n & ~(1 << k)

# Toggle kth bit
def toggle_bit(n, k):
    return n ^ (1 << k)

# Remove rightmost 1
def remove_rightmost_1(n):
    return n & (n - 1)

# Get rightmost 1
def get_rightmost_1(n):
    return n & -n

# Check if power of 2
def is_power_of_2(n):
    return n > 0 and (n & (n - 1)) == 0

# Count set bits (Brian Kernighan's)
def count_bits(n):
    count = 0
    while n:
        n &= n - 1
        count += 1
    return count
```

**Useful Patterns:**

### 1. Find Single Number (XOR)
```python
result = 0
for num in nums:
    result ^= num
return result
```

### 2. Add Without Arithmetic Operators
```python
def add(a, b):
    while b:
        carry = (a & b) << 1
        a = a ^ b
        b = carry
    return a
```

### 3. Swap Without Temp
```python
a ^= b
b ^= a
a ^= b
```

### 4. Check Even/Odd
```python
is_odd = n & 1
is_even = not (n & 1)
```

### 5. Multiply/Divide by 2
```python
n << 1  # Multiply by 2
n >> 1  # Divide by 2
```

**Bit Masks:**

```python
# Create mask with first n bits set
mask = (1 << n) - 1  # n=3: 111 (7)

# Check if bits in positions match
def bits_match(a, b, mask):
    return (a & mask) == (b & mask)

# Extract range of bits [i, j]
def extract_bits(n, i, j):
    return (n >> i) & ((1 << (j - i + 1)) - 1)
```

**Signed Integers:**
- Python handles arbitrary precision
- In languages with fixed size, be careful of:
  - Sign bit (MSB)
  - Two's complement representation
  - Overflow/underflow

**Two's Complement:**
- Negative number: flip bits + add 1
- `-n = ~n + 1`
- Range for k bits: `-2^(k-1)` to `2^(k-1) - 1`

**Time Complexity:**
- Single operation: O(1)
- Counting bits: O(log n) or O(number of 1's)
- Most bit tricks: O(1)

**Space Complexity:**
- Usually O(1) - just variables

**Common Patterns:**

1. **Finding Unique:** XOR all
2. **Counting Bits:** `n & (n-1)` trick
3. **Power of 2:** `n & (n-1) == 0`
4. **Get Lowest Bit:** `n & -n`
5. **Toggle/Set/Clear:** Use masks

**When to Use Bit Manipulation:**
- Finding unique elements with pairs
- Counting set bits
- Power of 2 checks
- Space optimization (bitmasks)
- Arithmetic without operators
- Subset generation

**Subset Generation (Bitmask):**
```python
n = 3
for mask in range(1 << n):  # 0 to 2^n - 1
    subset = []
    for i in range(n):
        if mask & (1 << i):
            subset.append(arr[i])
    print(subset)
```

**Common Mistakes:**
- Confusing `&` (AND) with `&&` (logical AND)
- Not handling negative numbers properly
- Forgetting precedence (`&` lower than `==`)
- Infinite loops with carries
- Not masking bits in fixed-width scenarios
- Sign extension issues in right shift

**Debugging Tips:**
- Print numbers in binary: `bin(n)`
- Visualize operations bit by bit
- Test with small numbers first
- Remember operator precedence

**Key Insights:**
- **XOR is self-inverse** - perfect for finding unique
- **`n & (n-1)`** removes rightmost 1 - count set bits
- **`n & -n`** extracts rightmost 1 - useful in many scenarios
- **Power of 2** has exactly one bit set
- Bit manipulation is **fast and space-efficient**
- Think in **binary representation**

**Advanced Applications:**
- Subset DP (bitmask DP)
- Optimization problems with states
- Graph coloring
- Set operations
- Compression

**Pattern Recognition:**
- Find unique with duplicates → XOR
- Count something → bit counting
- Power of 2 check → `n & (n-1)`
- No arithmetic operators → bit operations
- Generate all subsets → bitmask iteration

**Pro Tips:**
- Draw out bits on paper
- Test with powers of 2
- Remember: `1 << k` = 2^k
- XOR is your friend for pairs
- `& (n-1)` is magical for many operations
