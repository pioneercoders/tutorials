# Bit Manipulation

Bit manipulation involves operating on individual bits of binary numbers to solve problems efficiently. It leverages bitwise operators for fast computations.

## Introduction

Bit manipulation is a technique that operates directly on the binary representation of numbers to perform operations efficiently. It uses bitwise operators (AND, OR, XOR, NOT, shift) to manipulate individual bits, enabling extremely fast computations that often run in a single CPU cycle. Bit manipulation is essential for low-level programming, optimization, and solving problems that involve binary data, flags, permissions, and space-efficient storage.

**Why Bit Manipulation Exists:**
- Extremely fast operations (single CPU cycle)
- Space-efficient storage (bit packing)
- Direct hardware-level control
- Essential for low-level programming
- Elegant solutions to complex problems

**Where It Is Used:**
- Permission systems and access control
- Feature flags and configuration
- Data compression algorithms
- Cryptography and encryption
- Graphics and image processing
- Network protocols
- Embedded systems
- Algorithm optimization

## Core Concept Explanation

Bit manipulation works by operating on the binary representation of numbers. Each number is stored as a sequence of bits (0s and 1s), and bitwise operators allow us to manipulate these bits directly. The key operators are AND (`&`), OR (`|`), XOR (`^`), NOT (`~`), left shift (`<<`), and right shift (`>>`). Understanding these operators and how to use bit masks is fundamental to bit manipulation.

**Step-by-Step Breakdown:**
1. Understand binary representation of numbers
2. Learn bitwise operators (AND, OR, XOR, NOT, shift)
3. Create bit masks to target specific bits
4. Apply operations to set, clear, toggle, or check bits
5. Use bit manipulation for efficient algorithms
6. Handle edge cases (negative numbers, overflow)

**Intuition Behind the Concept:**
Think of a number as a row of light switches (bits). Each switch can be on (1) or off (0). Bit manipulation is like flipping these switches individually or in groups to achieve a desired pattern. For example, if you want to turn on the 3rd switch, you use a mask with only the 3rd bit set to 1.

**Visual Thinking:**
```
Binary Representation:

Decimal: 13
Binary:  1101 (8 + 4 + 0 + 1)

Bit Positions:
Position: 3  2  1  0
Bit:      1  1  0  1
Value:    8  4  0  1

Bitwise Operations:

AND (&): 1101 & 1010 = 1000 (8)
OR  (|): 1101 | 1010 = 1111 (15)
XOR (^): 1101 ^ 1010 = 0111 (7)
NOT (~): ~1101 = 0010 (2, assuming 4 bits)

Left Shift (<<): 1101 << 1 = 11010 (26)
Right Shift (>>): 1101 >> 1 = 110 (6)
```

## Internal Working / Logic

Bit manipulation operates through bitwise operators that work on the binary representation of numbers. Each operator performs a specific operation on each bit position independently.

**Operation 1: AND (&)**
- Returns 1 only if both bits are 1
- Used to check if bits are set
- Used to clear specific bits

**Operation 2: OR (|)**
- Returns 1 if either bit is 1
- Used to set specific bits
- Used to combine bit masks

**Operation 3: XOR (^)**
- Returns 1 if bits are different
- Used to toggle bits
- Used to find unique elements

**Operation 4: NOT (~)**
- Flips all bits (0 to 1, 1 to 0)
- Used for complement
- Watch for negative numbers

**Operation 5: Left Shift (`<<`)**
- Shifts bits left, fills with 0
- Equivalent to multiplying by 2^n
- Used for fast multiplication

**Operation 6: Right Shift (`>>`)**
- Shifts bits right, fills with sign bit
- Equivalent to dividing by 2^n
- Used for fast division

**Flow Explanation (Get Bit):**
1. Create mask with bit at position i set to 1
2. Shift number right by i positions
3. AND with 1 to isolate the bit
4. Return result (0 or 1)

**Decision Making Logic:**
The key decision is which operator to use:
- Use AND to check or clear bits
- Use OR to set bits
- Use XOR to toggle or find differences
- Use shift for multiplication/division
- Wrong operator leads to incorrect results

## Algorithm / Approach

**Get Bit Algorithm**

```
1. Shift number right by i positions
2. AND with 1 to isolate the bit
3. Return result (0 or 1)
```

**Set Bit Algorithm**

```
1. Create mask with bit at position i set to 1
2. OR number with mask
3. Return result
```

**Clear Bit Algorithm**

```
1. Create mask with bit at position i set to 1
2. Negate mask (NOT)
3. AND number with negated mask
4. Return result
```

**Toggle Bit Algorithm**

```
1. Create mask with bit at position i set to 1
2. XOR number with mask
3. Return result
```

**Count Set Bits Algorithm**

```
1. Initialize count to 0
2. While number is not 0:
   a. AND number with (number - 1)
   b. Increment count
3. Return count
```

## Implementations

### 1. Get Bit

```javascript
function getBit(num, i) {
  return (num >> i) & 1;
}
```

**Advantages:**
- O(1) time
- Simple and fast
- Single operation

### 2. Set Bit

```javascript
function setBit(num, i) {
  return num | (1 << i);
}
```

**Advantages:**
- O(1) time
- Uses OR operator
- Preserves other bits

### 3. Clear Bit

```javascript
function clearBit(num, i) {
  return num & ~(1 << i);
}
```

**Advantages:**
- O(1) time
- Uses AND with negated mask
- Preserves other bits

### 4. Toggle Bit

```javascript
function toggleBit(num, i) {
  return num ^ (1 << i);
}
```

**Advantages:**
- O(1) time
- Uses XOR operator
- Flips specific bit

### 5. Count Set Bits

```javascript
function countSetBits(n) {
  let count = 0;
  while (n !== 0) {
    n &= n - 1; // Clears the rightmost set bit
    count++;
  }
  return count;
}
```

**Advantages:**
- O(k) time where k is number of set bits
- Brian Kernighan's algorithm
- Efficient for sparse bit patterns

### 6. Single Number

```javascript
function singleNumber(nums) {
  let result = 0;
  for (const num of nums) {
    result ^= num;
  }
  return result;
}
```

**Advantages:**
- O(n) time, O(1) space
- Uses XOR property
- Elegant solution

### 7. Power of Two

```javascript
function isPowerOfTwo(n) {
  return n > 0 && (n & (n - 1)) === 0;
}
```

**Advantages:**
- O(1) time
- Uses bit property
- Powers of two have single set bit

### 8. Swap Numbers

```javascript
function swapNumbers(a, b) {
  a ^= b;
  b ^= a;
  a ^= b;
  return [a, b];
}
```

**Advantages:**
- O(1) time, O(1) space
- No temporary variable
- Uses XOR property

## Dry Run

**Example: Count Set Bits of 13**

**Input:**
```
n = 13 (binary: 1101)
```

**Step-by-Step Execution:**

```
Initial State:
n = 13 (1101)
count = 0

Iteration 1:
n = 13 (1101)
n - 1 = 12 (1100)
n & (n - 1) = 1101 & 1100 = 1100 (12)
n = 12
count = 1

Iteration 2:
n = 12 (1100)
n - 1 = 11 (1011)
n & (n - 1) = 1100 & 1011 = 1000 (8)
n = 8
count = 2

Iteration 3:
n = 8 (1000)
n - 1 = 7 (0111)
n & (n - 1) = 1000 & 0111 = 0000 (0)
n = 0
count = 3

Final: count = 3
```

**Variable Changes Table:**

| Iteration | n (binary) | n - 1 (binary) | n & (n-1) (binary) | n (decimal) | count |
|-----------|------------|----------------|-------------------|-------------|-------|
| 1 | 1101 | 1100 | 1100 | 12 | 1 |
| 2 | 1100 | 1011 | 1000 | 8 | 2 |
| 3 | 1000 | 0111 | 0000 | 0 | 3 |

## Edge Cases

### 1. Negative Numbers
```javascript
n = -1
Binary: all 1s (two's complement)
countSetBits(-1) → 32 (in 32-bit system)
Handle with unsigned or specific logic
```

### 2. Zero
```javascript
n = 0
Binary: 0000
countSetBits(0) → 0
No set bits
```

### 3. Single Bit Set
```javascript
n = 1
Binary: 0001
countSetBits(1) → 1
Only one set bit
```

### 4. All Bits Set
```javascript
n = 255 (11111111)
countSetBits(255) → 8
All 8 bits set
```

### 5. Overflow
```javascript
1 << 31
May overflow in some languages
Handle with BigInt or checks
```

### 6. Swap Same Number
```javascript
a = 5, b = 5
swapNumbers(5, 5) → [0, 0]
XOR with same number gives 0
```

**Why Edge Cases Matter:**
- Negative numbers use two's complement
- Zero is a special case
- Overflow can cause errors
- Same numbers XOR to 0
- Must handle gracefully

## Variations / Extensions

### 1. Find Missing Number

```javascript
function missingNumber(nums) {
  let n = nums.length;
  let xor = 0;
  
  for (let i = 0; i <= n; i++) {
    xor ^= i;
  }
  
  for (const num of nums) {
    xor ^= num;
  }
  
  return xor;
}
```

### 2. Reverse Bits

```javascript
function reverseBits(n) {
  let result = 0;
  for (let i = 0; i < 32; i++) {
    result = (result << 1) | (n & 1);
    n >>= 1;
  }
  return result >>> 0;
}
```

### 3. Hamming Distance

```javascript
function hammingDistance(x, y) {
  let xor = x ^ y;
  let distance = 0;
  
  while (xor !== 0) {
    xor &= xor - 1;
    distance++;
  }
  
  return distance;
}
```

### 4. Find Two Unique Numbers

```javascript
function singleNumberIII(nums) {
  let xor = 0;
  for (const num of nums) {
    xor ^= num;
  }
  
  let rightmost = xor & -xor;
  let a = 0, b = 0;
  
  for (const num of nums) {
    if (num & rightmost) {
      a ^= num;
    } else {
      b ^= num;
    }
  }
  
  return [a, b];
}
```

### 5. Add Without Plus

```javascript
function addWithoutPlus(a, b) {
  while (b !== 0) {
    const carry = a & b;
    a = a ^ b;
    b = carry << 1;
  }
  return a;
}
```

## Optimization Techniques

### 1. Bit Tricks

**Fast Operations:**
```javascript
// Check if even: n & 1 === 0
// Check if power of two: n & (n-1) === 0
// Swap without temp: a ^= b; b ^= a; a ^= b
// Absolute value: (n ^ (n >> 31)) - (n >> 31)
```

### 2. Lookup Tables

**Precompute Results:**
```javascript
// Precompute bit counts for bytes
// O(1) lookup instead of O(k)
// Trade space for time
```

### 3. Trade-offs

**Bit Manipulation vs Arithmetic:**

| Aspect | Bit Manipulation | Arithmetic |
|--------|------------------|------------|
| Speed | Single cycle | Multiple cycles |
| Readability | Low | High |
| Space | Efficient | Normal |
| Portability | Platform dependent | Portable |
| Best For | Low-level ops | General purpose |

**When to Use Bit Manipulation:**
- Performance is critical
- Working with binary data
- Need space efficiency
- Low-level programming

## Complexity Analysis

### Time Complexity

**Bit Operations: O(1)**
- Single CPU cycle
- Constant time
- Example: Get, set, clear bit

**Count Set Bits: O(k)**
- k = number of set bits
- Brian Kernighan's algorithm
- Example: countSetBits

**Reverse Bits: O(n)**
- n = number of bits
- Process each bit
- Example: reverseBits

### Space Complexity

**Most Operations: O(1)**
- No extra space
- In-place operations
- Example: All bit operations

**Lookup Table: O(2^n)**
- Precompute all results
- Trade space for time
- Example: Bit count table

**Explanation:**
Bit operations are O(1) because they operate on fixed-size integers. Operations that process all bits are O(n) where n is the number of bits. Space is typically O(1) for in-place operations.

## Real-world Applications

### 1. Permission Systems

**Access Control:**
- Bit flags for permissions
- Efficient storage
- Example: Read, write, execute flags

### 2. Feature Flags

**Configuration:**
- Enable/disable features
- Space-efficient storage
- Example: A/B testing flags

### 3. Data Compression

**Compression Algorithms:**
- Huffman coding
- Run-length encoding
- Example: ZIP compression

### 4. Cryptography

**Encryption:**
- Bit-level operations
- XOR for encryption
- Example: One-time pad

### 5. Graphics

**Image Processing:**
- Pixel manipulation
- Color channel operations
- Example: Image filters

### 6. Network Protocols

**Packet Processing:**
- Header parsing
- Flag checking
- Example: TCP flags

### 7. Embedded Systems

**Hardware Control:**
- Register manipulation
- GPIO control
- Example: Microcontroller programming

### 8. Game Development

**State Management:**
- Bit masks for states
- Collision detection
- Example: Game flags

## Common Mistakes

### 1. Operator Precedence

**Mistake:**
```javascript
// Wrong precedence
result = num & 1 << i; // Wrong! (num & 1) << i
```

**Correct:**
```javascript
// Use parentheses
result = (num >> i) & 1; // Correct
```

**Why It Matters:**
- Bitwise operators have low precedence
- Without parentheses, wrong result
- Always use parentheses

### 2. Not Handling Negative Numbers

**Mistake:**
```javascript
// Not handling two's complement
countSetBits(-1) // May give unexpected result
```

**Correct:**
```javascript
// Handle negative numbers
// Use unsigned or specific logic
```

**Why It Matters:**
- Negative numbers use two's complement
- All bits are set for -1
- Must handle specially

### 3. Overflow

**Mistake:**
```javascript
// May overflow
1 << 31 // Overflow in 32-bit system
```

**Correct:**
```javascript
// Use BigInt or check
BigInt(1) << 31n
```

**Why It Matters:**
- Shift can cause overflow
- Results are undefined
- Must check bounds

### 4. Confusing XOR with OR

**Mistake:**
```javascript
// Using OR instead of XOR
num | mask // Sets bit, doesn't toggle
```

**Correct:**
```javascript
// Use XOR to toggle
num ^ mask // Toggles bit
```

**Why It Matters:**
- OR sets bit to 1
- XOR flips bit
- Wrong operator, wrong result

### 5. Not Using Unsigned

**Mistake:**
```javascript
// Signed right shift
n >> 1 // Fills with sign bit
```

**Correct:**
```javascript
// Unsigned right shift
n >>> 1 // Fills with 0
```

**Why It Matters:**
- Signed shift fills with sign bit
- Unsigned shift fills with 0
- Different results for negative numbers

### 6. Forgetting to Mask

**Mistake:**
```javascript
// Not masking after shift
num >> i // Still has other bits
```

**Correct:**
```javascript
// Mask to isolate bit
(num >> i) & 1 // Isolates the bit
```

**Why It Matters:**
- Shift doesn't isolate bit
- Must AND with 1
- Otherwise wrong result

## Advanced Concepts

### 1. Bit Masks

**Concept:**
Use masks to target specific bits.

**Features:**
- Combine multiple flags
- Efficient storage
- Used in permission systems

### 2. Two's Complement

**Concept:**
Representation of negative numbers.

**Features:**
- Invert bits and add 1
- Most common representation
- Used in most systems

### 3. Endianness

**Concept:**
Byte order in multi-byte values.

**Features:**
- Little-endian vs big-endian
- Platform dependent
- Important for network protocols

### 4. Bit Fields

**Concept:**
Pack multiple values into one integer.

**Features:**
- Space-efficient storage
- Used in embedded systems
- Requires careful bit manipulation

## Practice Thinking Guide

### How to Identify When to Use Bit Manipulation

**Key Signals in Problem Statements:**

1. **"Single/unique element"**
   - XOR property
   - Example: "Single number"

2. **"Power of two"**
   - Bit property
   - Example: "Power of two"

3. **"Set/clear/toggle bits"**
   - Bit operations
   - Example: "Flip bits"

4. **"Count set bits"**
   - Bit counting
   - Example: "Hamming weight"

5. **"Binary representation"**
   - Direct bit manipulation
   - Example: "Reverse bits"

6. **"Without arithmetic operators"**
   - Bit manipulation only
   - Example: "Add without plus"

**Pattern Recognition:**

**Pattern 1: Unique Element**
```
Problem: Find unique element
Solution: XOR all elements
```

**Pattern 2: Power of Two**
```
Problem: Check power of two
Solution: n & (n-1) === 0
```

**Pattern 3: Count Set Bits**
```
Problem: Count set bits
Solution: Brian Kernighan's algorithm
```

**Pattern 4: Missing Number**
```
Problem: Find missing number
Solution: XOR with indices
```

**Pattern 5: Swap Without Temp**
```
Problem: Swap without temp
Solution: XOR swap
```

**Decision Flowchart:**

```
Involves binary/bits?
├─ Yes → Need fast operations?
│        ├─ Yes → Use bit manipulation
│        └─ No → Consider other
├─ No → Need space efficiency?
│        ├─ Yes → Use bit manipulation
│        └─ No → Consider other
└─ No → Not bit manipulation problem
```

**Example Problem Analysis:**

**Problem:** "Find single number in array where all others appear twice"

**Analysis:**
1. Need to find unique element
2. XOR property: a ^ a = 0, a ^ 0 = a
3. XOR all elements cancels pairs
4. Remaining is unique element
5. Solution: XOR all elements

**Problem:** "Check if number is power of two"

**Analysis:**
1. Powers of two have single set bit
2. n & (n-1) clears rightmost set bit
3. If result is 0, power of two
4. O(1) time, O(1) space
5. Solution: n & (n-1) === 0

**Problem:** "Count set bits in number"

**Analysis:**
1. Need to count 1s in binary
2. Brian Kernighan's algorithm
3. n & (n-1) clears rightmost set bit
4. Count until n is 0
5. Solution: n & (n-1) loop

## Summary

Bit manipulation is a powerful technique for operating directly on binary representations of numbers. It enables extremely fast operations, space-efficient storage, and elegant solutions to complex problems. Understanding bitwise operators, bit masks, and common bit tricks is essential for low-level programming and algorithm optimization.

**Key Takeaways:**
- Bit operations are extremely fast
- Understand bitwise operators
- Use bit masks for specific bits
- XOR property for unique elements
- n & (n-1) for power of two
- Handle negative numbers carefully
- Watch for operator precedence
- Platform-dependent behavior

**Mastery Checklist:**
- ✅ Understand binary representation
- ✅ Know bitwise operators
- ✅ Implement get/set/clear/toggle bit
- ✅ Count set bits efficiently
- ✅ Use XOR for unique elements
- ✅ Check power of two
- ✅ Handle negative numbers
- ✅ Know when to use bit manipulation

