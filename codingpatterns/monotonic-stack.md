# Monotonic Stack

Monotonic stack is a stack that maintains elements in either increasing or decreasing order. It's used to find next greater/smaller elements efficiently.

## Introduction

Monotonic stack is a specialized stack data structure that maintains elements in either strictly increasing or strictly decreasing order. Unlike a regular stack where elements can be in any order, a monotonic stack enforces a specific ordering property. This property makes it extremely efficient for solving problems that involve finding the next greater or smaller element, calculating ranges, and detecting boundaries. The key insight is that by maintaining order, we can avoid the O(n²) brute force approach and achieve O(n) time complexity.

**Why Monotonic Stack Exists:**
- Finding next greater/smaller element requires O(n²) with brute force
- Monotonic stack reduces this to O(n) by maintaining order
- Elegant solution for range and boundary problems
- Foundation for more complex algorithms
- Used in financial analysis, inventory management, and more

**Where It Is Used:**
- Stock price analysis (next higher price)
- Daily temperature tracking (next warmer day)
- Histogram area calculations
- Inventory management (stock levels)
- Range queries and boundary detection
- Sliding window maximum/minimum
- Financial time-series analysis
- Activity feed ranking

## Core Concept Explanation

A monotonic stack maintains elements in either increasing or decreasing order. For a decreasing monotonic stack, we pop elements from the stack when we encounter a larger element, ensuring the stack always contains elements in decreasing order. For an increasing monotonic stack, we pop elements when we encounter a smaller element. This property allows us to efficiently find the next greater or smaller element for each element in a single pass through the array.

**Step-by-Step Breakdown:**
1. Initialize an empty stack
2. Iterate through the array
3. For each element:
   - While stack is not empty and current element violates monotonic property:
     - Pop from stack
     - Process popped element (e.g., set its next greater element)
   - Push current element onto stack
4. Process remaining elements in stack (no next greater/smaller found)

**Intuition Behind the Concept:**
Think of people standing in line sorted by height. If you want to find the next taller person for each person, you can maintain a line where people are arranged in decreasing height. When a new person arrives who is taller than some in line, those shorter people now have their "next taller person" and can leave the line. This way, each person only needs to check the person in front of them, not everyone behind.

**Visual Thinking:**
```
Monotonic Decreasing Stack for Next Greater Element:

Array: [2, 1, 2, 4, 3]

Step 1: Process 2
Stack: [2] (indices)

Step 2: Process 1
1 < 2, maintain decreasing order
Stack: [2, 1]

Step 3: Process 2
2 > 1, pop 1 (next greater of 1 is 2)
2 == 2, keep (depending on strictness)
Stack: [2, 2]

Step 4: Process 4
4 > 2, pop 2 (next greater of 2 is 4)
4 > 2, pop 2 (next greater of 2 is 4)
Stack: [4]

Step 5: Process 3
3 < 4, maintain decreasing order
Stack: [4, 3]

Final Stack: [4, 3] (no next greater for these)
Result: [4, 2, 4, -1, -1]
```

## Internal Working / Logic

Monotonic stack operates by maintaining the monotonic property through push and pop operations. The key is that we only push elements that maintain the order, and we pop elements when the current element violates the order. This ensures that each element is pushed and popped at most once, giving O(n) time complexity.

**Operation 1: Decreasing Monotonic Stack**
- Maintain elements in decreasing order
- Pop when current element is greater than stack top
- Used for finding next greater element
- Example: Daily temperatures, stock prices

**Operation 2: Increasing Monotonic Stack**
- Maintain elements in increasing order
- Pop when current element is smaller than stack top
- Used for finding next smaller element
- Example: Histogram area, trapping rain water

**Operation 3: Handling Equal Elements**
- Strict monotonic: pop when equal
- Non-strict: keep when equal
- Depends on problem requirements
- Important for correctness

**Flow Explanation (Next Greater Element):**
1. Initialize empty stack and result array with -1
2. For each element in array:
   - While stack not empty and current > stack top:
     - Pop index from stack
     - Set result[popped] = current
   - Push current index onto stack
3. Return result (remaining indices have -1)

**Decision Making Logic:**
The key decision is increasing vs decreasing:
- Use decreasing stack for next greater element
- Use increasing stack for next smaller element
- Use decreasing stack for histogram area
- Use increasing stack for trapping rain water
- Handle equal elements based on problem

## Algorithm / Approach

**Next Greater Element Algorithm**

```
1. Initialize empty stack and result array with -1
2. For each element in array:
   a. While stack not empty and current > stack top:
      i. Pop index from stack
      ii. Set result[popped] = current
   b. Push current index onto stack
3. Return result
```

**Daily Temperatures Algorithm**

```
1. Initialize empty stack and result array with 0
2. For each day with temperature:
   a. While stack not empty and current > stack top:
      i. Pop index from stack
      ii. Set result[popped] = current index - popped index
   b. Push current index onto stack
3. Return result
```

**Largest Rectangle in Histogram Algorithm**

```
1. Initialize empty stack and max_area = 0
2. Append 0 to heights (sentinel)
3. For each index with height:
   a. While stack not empty and current < stack top:
      i. Pop height from stack
      ii. Calculate width
      iii. Update max_area
   b. Push current index onto stack
4. Return max_area
```

**Next Greater Element II (Circular) Algorithm**

```
1. Initialize empty stack and result array with -1
2. Iterate through array twice (2n iterations):
   a. Use modulo for circular index
   b. While stack not empty and current > stack top:
      i. Pop index from stack
      ii. Set result[popped] = current (if not set)
   c. Push current index onto stack
3. Return result
```

## Implementations

### 1. Next Greater Element

```javascript
function nextGreaterElement(nums) {
  const n = nums.length;
  const result = new Array(n).fill(-1);
  const stack = [];
  
  for (let i = 0; i < n; i++) {
    while (stack.length > 0 && nums[i] > nums[stack[stack.length - 1]]) {
      const idx = stack.pop();
      result[idx] = nums[i];
    }
    stack.push(i);
  }
  
  return result;
}
```

**Advantages:**
- O(n) time complexity
- O(n) space complexity
- Each element pushed/popped at most once

### 2. Daily Temperatures

```javascript
function dailyTemperatures(temperatures) {
  const n = temperatures.length;
  const result = new Array(n).fill(0);
  const stack = [];
  
  for (let i = 0; i < n; i++) {
    while (stack.length > 0 && temperatures[i] > temperatures[stack[stack.length - 1]]) {
      const idx = stack.pop();
      result[idx] = i - idx;
    }
    stack.push(i);
  }
  
  return result;
}
```

**Advantages:**
- O(n) time complexity
- Tracks days until warmer temperature
- Practical real-world application

### 3. Largest Rectangle in Histogram

```javascript
function largestRectangleArea(heights) {
  const stack = [];
  let maxArea = 0;
  heights.push(0); // Sentinel to force final calculation
  
  for (let i = 0; i < heights.length; i++) {
    while (stack.length > 0 && heights[i] < heights[stack[stack.length - 1]]) {
      const height = heights[stack.pop()];
      const width = stack.length === 0 ? i : i - stack[stack.length - 1] - 1;
      maxArea = Math.max(maxArea, height * width);
    }
    stack.push(i);
  }
  
  heights.pop();
  return maxArea;
}
```

**Advantages:**
- O(n) time complexity
- Uses sentinel for edge case
- Calculates maximum rectangle area

### 4. Next Greater Element II (Circular)

```javascript
function nextGreaterElementII(nums) {
  const n = nums.length;
  const result = new Array(n).fill(-1);
  const stack = [];
  
  for (let i = 0; i < 2 * n; i++) {
    const idx = i % n;
    while (stack.length > 0 && nums[idx] > nums[stack[stack.length - 1]]) {
      const popped = stack.pop();
      if (result[popped] === -1) {
        result[popped] = nums[idx];
      }
    }
    stack.push(idx);
  }
  
  return result;
}
```

**Advantages:**
- Handles circular arrays
- O(n) time complexity
- Each element processed at most twice

### 5. Next Smaller Element

```javascript
function nextSmallerElement(nums) {
  const n = nums.length;
  const result = new Array(n).fill(-1);
  const stack = [];
  
  for (let i = 0; i < n; i++) {
    while (stack.length > 0 && nums[i] < nums[stack[stack.length - 1]]) {
      const idx = stack.pop();
      result[idx] = nums[i];
    }
    stack.push(i);
  }
  
  return result;
}
```

**Advantages:**
- Increasing monotonic stack
- Finds next smaller element
- O(n) time complexity

## Dry Run

**Example: Next Greater Element**

**Input:**
```
nums = [2, 1, 2, 4, 3]
```

**Step-by-Step Execution:**

```
Initial State:
stack = []
result = [-1, -1, -1, -1, -1]

Iteration 1: i = 0, nums[0] = 2
stack is empty, push 0
stack = [0]
result = [-1, -1, -1, -1, -1]

Iteration 2: i = 1, nums[1] = 1
nums[1] (1) < nums[stack[-1]] (nums[0] = 2)
Push 1
stack = [0, 1]
result = [-1, -1, -1, -1, -1]

Iteration 3: i = 2, nums[2] = 2
nums[2] (2) > nums[stack[-1]] (nums[1] = 1)
Pop 1, result[1] = 2
stack = [0]
nums[2] (2) == nums[stack[-1]] (nums[0] = 2)
Push 2 (non-strict)
stack = [0, 2]
result = [-1, 2, -1, -1, -1]

Iteration 4: i = 3, nums[3] = 4
nums[3] (4) > nums[stack[-1]] (nums[2] = 2)
Pop 2, result[2] = 4
stack = [0]
nums[3] (4) > nums[stack[-1]] (nums[0] = 2)
Pop 0, result[0] = 4
stack = []
Push 3
stack = [3]
result = [4, 2, 4, -1, -1]

Iteration 5: i = 4, nums[4] = 3
nums[4] (3) < nums[stack[-1]] (nums[3] = 4)
Push 4
stack = [3, 4]
result = [4, 2, 4, -1, -1]

Final: result = [4, 2, 4, -1, -1]
```

**Variable Changes Table:**

| Iteration | i | nums[i] | stack (after) | result (after) |
|-----------|---|---------|---------------|----------------|
| 1 | 0 | 2 | [0] | [-1, -1, -1, -1, -1] |
| 2 | 1 | 1 | [0, 1] | [-1, -1, -1, -1, -1] |
| 3 | 2 | 2 | [0, 2] | [-1, 2, -1, -1, -1] |
| 4 | 3 | 4 | [3] | [4, 2, 4, -1, -1] |
| 5 | 4 | 3 | [3, 4] | [4, 2, 4, -1, -1] |

## Edge Cases

### 1. Empty Array
```javascript
nums = []
nextGreaterElement([]) → []
Handle empty input gracefully
```

### 2. Single Element
```javascript
nums = [5]
nextGreaterElement([5]) → [-1]
No next greater element
```

### 3. All Equal Elements
```javascript
nums = [2, 2, 2]
nextGreaterElement([2, 2, 2]) → [-1, -1, -1]
Depends on strictness
```

### 4. Strictly Increasing
```javascript
nums = [1, 2, 3, 4]
nextGreaterElement([1, 2, 3, 4]) → [2, 3, 4, -1]
Each element has next greater
```

### 5. Strictly Decreasing
```javascript
nums = [4, 3, 2, 1]
nextGreaterElement([4, 3, 2, 1]) → [-1, -1, -1, -1]
No next greater elements
```

### 6. Circular Array
```javascript
nums = [1, 2, 1]
nextGreaterElementII([1, 2, 1]) → [2, -1, 2]
Wrap-around to find next greater
```

**Why Edge Cases Matter:**
- Empty array needs special handling
- Single element is base case
- Equal elements depend on strictness
- Strictly increasing/decreasing test boundaries
- Circular arrays need modulo operation

## Variations / Extensions

### 1. Previous Greater Element

```javascript
function previousGreaterElement(nums) {
  const n = nums.length;
  const result = new Array(n).fill(-1);
  const stack = [];
  
  for (let i = 0; i < n; i++) {
    while (stack.length > 0 && nums[stack[stack.length - 1]] <= nums[i]) {
      stack.pop();
    }
    result[i] = stack.length > 0 ? nums[stack[stack.length - 1]] : -1;
    stack.push(i);
  }
  
  return result;
}
```

### 2. Trapping Rain Water

```javascript
function trap(height) {
  const stack = [];
  let water = 0;
  
  for (let i = 0; i < height.length; i++) {
    while (stack.length > 0 && height[i] > height[stack[stack.length - 1]]) {
      const mid = stack.pop();
      if (stack.length === 0) break;
      const left = stack[stack.length - 1];
      const right = i;
      const h = Math.min(height[left], height[right]) - height[mid];
      water += h * (right - left - 1);
    }
    stack.push(i);
  }
  
  return water;
}
```

### 3. Remove Duplicate Letters

```javascript
function removeDuplicateLetters(s) {
  const count = {};
  for (const char of s) {
    count[char] = (count[char] || 0) + 1;
  }
  
  const visited = new Set();
  const stack = [];
  
  for (const char of s) {
    count[char]--;
    if (visited.has(char)) continue;
    
    while (stack.length > 0 && char < stack[stack.length - 1] && count[stack[stack.length - 1]] > 0) {
      visited.delete(stack.pop());
    }
    
    stack.push(char);
    visited.add(char);
  }
  
  return stack.join('');
}
```

### 4. Car Fleet

```javascript
function carFleet(target, position, speed) {
  const cars = position.map((pos, i) => ({ pos, speed: speed[i] }));
  cars.sort((a, b) => b.pos - a.pos);
  
  const stack = [];
  
  for (const car of cars) {
    const time = (target - car.pos) / car.speed;
    while (stack.length > 0 && time >= stack[stack.length - 1]) {
      stack.pop();
    }
    stack.push(time);
  }
  
  return stack.length;
}
```

### 5. Sliding Window Maximum

```javascript
function maxSlidingWindow(nums, k) {
  const result = [];
  const deque = [];
  
  for (let i = 0; i < nums.length; i++) {
    while (deque.length > 0 && deque[0] <= i - k) {
      deque.shift();
    }
    
    while (deque.length > 0 && nums[i] >= nums[deque[deque.length - 1]]) {
      deque.pop();
    }
    
    deque.push(i);
    
    if (i >= k - 1) {
      result.push(nums[deque[0]]);
    }
  }
  
  return result;
}
```

## Optimization Techniques

### 1. Sentinel Values

**Force Final Processing:**
```javascript
// Append 0 to heights
// Forces all remaining calculations
// Clean boundary handling
```

### 2. Early Termination

**Stop When Possible:**
```javascript
// Break when stack empty
// No more elements to process
// Saves unnecessary iterations
```

### 3. Space Optimization

**Reuse Arrays:**
```javascript
// Use input array for storage
// Modify in-place if allowed
// Reduce space usage
```

### 4. Trade-offs

**Monotonic Stack vs Brute Force:**

| Aspect | Monotonic Stack | Brute Force |
|--------|-----------------|-------------|
| Time | `O(n)` | `O(n²)` |
| Space | `O(n)` | `O(1)` |
| Complexity | Medium | Simple |
| Best For | Large datasets | Small datasets |

**When to Use Monotonic Stack:**
- Need next greater/smaller element
- Range or boundary problems
- Large datasets
- O(n) time required

## Complexity Analysis

### Time Complexity

**Next Greater Element: O(n)**
- Each element pushed once
- Each element popped once
- Total operations: 2n
- Example: nextGreaterElement

**Daily Temperatures: O(n)**
- Each day pushed once
- Each day popped once
- Total operations: 2n
- Example: dailyTemperatures

**Largest Rectangle: O(n)**
- Each bar pushed once
- Each bar popped once
- Total operations: 2n
- Example: largestRectangleArea

**Circular Next Greater: O(2n)**
- Each element processed twice
- Still O(n) amortized
- Example: nextGreaterElementII

### Space Complexity

**Space: O(n)**
- Stack stores up to n elements
- Result array stores n elements
- Total: O(n)
- Example: All implementations

**Explanation:**
Monotonic stack achieves O(n) time complexity because each element is pushed and popped at most once. This is the key insight - the total number of push and pop operations is bounded by 2n. Space complexity is O(n) for the stack and result array.

## Real-world Applications

### 1. Stock Price Analysis

**Financial Trading:**
- Find next higher price
- Calculate profit opportunities
- Technical analysis
- Example: Stock trading algorithms

### 2. Daily Temperature Tracking

**Weather Forecasting:**
- Predict next warmer day
- Track temperature trends
- Seasonal analysis
- Example: Weather apps

### 3. Inventory Management

**Stock Control:**
- Monitor stock levels
- Predict shortages
- Optimize inventory
- Example: Warehouse management

### 4. Histogram Analysis

**Data Visualization:**
- Calculate maximum area
- Analyze distributions
- Statistical analysis
- Example: Image processing

### 5. Activity Feed Ranking

**Social Media:**
- Rank posts by engagement
- Find trending content
- Feed optimization
- Example: Facebook timeline

### 6. Range Queries

**Database Optimization:**
- Efficient range queries
- Boundary detection
- Index optimization
- Example: SQL optimization

### 7. Time-Series Analysis

**Data Analytics:**
- Find peaks and valleys
- Trend analysis
- Anomaly detection
- Example: Sensor data

### 8. Threshold Detection

**Monitoring Systems:**
- Detect threshold breaches
- Alert systems
- Performance monitoring
- Example: Server monitoring

## Common Mistakes

### 1. Not Maintaining Monotonic Property

**Mistake:**
```javascript
// Not popping when property violated
while (stack.length > 0 && condition) {
  // Missing pop operation
}
```

**Correct:**
```javascript
// Always pop when property violated
while (stack.length > 0 && condition) {
  stack.pop();
}
```

**Why It Matters:**
- Violates monotonic property
- Breaks algorithm correctness
- Must maintain order

### 2. Incorrect Boundary Handling

**Mistake:**
```javascript
// Not handling empty stack
const height = heights[stack.pop()]; // May be undefined
```

**Correct:**
```javascript
// Check stack before popping
if (stack.length > 0) {
  const height = heights[stack.pop()];
}
```

**Why It Matters:**
- Empty stack causes errors
- Boundary conditions critical
- Must check before access

### 3. Forgetting Sentinel

**Mistake:**
```javascript
// No sentinel for final calculation
// Remaining elements not processed
```

**Correct:**
```javascript
// Add sentinel to force final calculation
heights.push(0);
```

**Why It Matters:**
- Remaining elements need processing
- Sentinel forces final calculation
- Ensures complete solution

### 4. Wrong Monotonic Direction

**Mistake:**
```javascript
// Using increasing for next greater
// Should use decreasing
```

**Correct:**
```javascript
// Use decreasing for next greater
// Use increasing for next smaller
```

**Why It Matters:**
- Wrong direction gives wrong results
- Must match problem requirements
- Critical for correctness

### 5. Not Handling Circular Arrays

**Mistake:**
```javascript
// Single pass for circular array
// Doesn't handle wrap-around
```

**Correct:**
```javascript
// Double pass with modulo
for (let i = 0; i < 2 * n; i++) {
  const idx = i % n;
}
```

**Why It Matters:**
- Circular arrays need wrap-around
- Single pass insufficient
- Modulo operation required

### 6. Equal Elements Handling

**Mistake:**
```javascript
// Not handling equal elements correctly
// Strict vs non-strict matters
```

**Correct:**
```javascript
// Handle based on problem requirements
// Use >= or > based on strictness
```

**Why It Matters:**
- Equal elements affect results
- Strictness depends on problem
- Must handle correctly

## Advanced Concepts

### 1. Monotonic Queue

**Concept:**
Monotonic structure for sliding window.

**Features:**
- Deque instead of stack
- Sliding window maximum
- O(n) time complexity

### 2. Monotonic Deque

**Concept:**
Double-ended monotonic structure.

**Features:**
- Push and pop from both ends
- More flexible than stack
- Used in sliding window

### 3. Circular Arrays

**Concept:**
Arrays that wrap around.

**Features:**
- Use modulo operation
- Double pass processing
- Handle wrap-around

### 4. Multiple Passes

**Concept:**
Process array multiple times.

**Features:**
- For complex problems
- Combine multiple monotonic stacks
- Handle dependencies

## Practice Thinking Guide

### How to Identify When to Use Monotonic Stack

**Key Signals in Problem Statements:**

1. **"Next greater/smaller"**
   - Monotonic stack
   - Example: "Next greater element"

2. **"Next warmer/colder"**
   - Monotonic stack
   - Example: "Daily temperatures"

3. **"Maximum area"**
   - Monotonic stack
   - Example: "Largest rectangle"

4. **"Range" or "boundary"**
   - Monotonic stack
   - Example: "Boundary detection"

5. **"Circular"**
   - Monotonic stack with modulo
   - Example: "Circular array"

6. **"Histogram"**
   - Monotonic stack
   - Example: "Histogram area"

**Pattern Recognition:**

**Pattern 1: Next Greater Element**
```
Problem: Find next greater element
Solution: Decreasing monotonic stack
```

**Pattern 2: Daily Temperatures**
```
Problem: Days until warmer
Solution: Decreasing monotonic stack with indices
```

**Pattern 3: Largest Rectangle**
```
Problem: Maximum rectangle in histogram
Solution: Increasing monotonic stack with sentinel
```

**Pattern 4: Trapping Rain Water**
```
Problem: Calculate trapped water
Solution: Monotonic stack with height calculations
```

**Pattern 5: Circular Next Greater**
```
Problem: Next greater in circular array
Solution: Double pass with modulo
```

**Decision Flowchart:**

```
Involves next greater/smaller?
├─ Yes → Use monotonic stack
│        ├─ Greater? → Decreasing stack
│        └─ Smaller? → Increasing stack
├─ No → Involves area/boundary?
│        ├─ Yes → Use monotonic stack
│        └─ No → Consider other
└─ No → Not monotonic stack problem
```

**Example Problem Analysis:**

**Problem:** "Find next greater element for each element"

**Analysis:**
1. Need next greater element
2. Brute force O(n²)
3. Monotonic stack O(n)
4. Use decreasing stack
5. Solution: Decreasing monotonic stack

**Problem:** "Days until warmer temperature"

**Analysis:**
1. Need days until warmer
2. Similar to next greater
3. Track indices for distance
4. Decreasing monotonic stack
5. Solution: Decreasing stack with indices

**Problem:** "Largest rectangle in histogram"

**Analysis:**
1. Need maximum rectangle area
2. Find boundaries for each bar
3. Increasing monotonic stack
4. Use sentinel for final calculation
5. Solution: Increasing stack with sentinel

## Summary

Monotonic stack is a specialized stack that maintains elements in either increasing or decreasing order. It provides O(n) time complexity for problems involving next greater/smaller elements, range calculations, and boundary detection. The key insight is that each element is pushed and popped at most once, making it extremely efficient. Monotonic stacks are essential for financial analysis, inventory management, and various algorithmic problems.

**Key Takeaways:**
- Maintain monotonic property (increasing/decreasing)
- O(n) time complexity
- Each element pushed/popped at most once
- Use decreasing for next greater
- Use increasing for next smaller
- Handle equal elements based on strictness
- Use sentinel for boundary cases
- Circular arrays need modulo operation

**Mastery Checklist:**
- ✅ Understand monotonic property
- ✅ Implement next greater element
- ✅ Implement daily temperatures
- ✅ Implement largest rectangle
- ✅ Handle circular arrays
- ✅ Use sentinel values
- ✅ Handle equal elements
- ✅ Choose increasing vs decreasing
