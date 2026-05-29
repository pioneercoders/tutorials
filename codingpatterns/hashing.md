# Hashing

Hashing is a technique that maps data of arbitrary size to fixed-size values using a hash function. It enables O(1) average time complexity for insert, delete, and search operations.

## Introduction

Hashing is a fundamental technique in computer science that maps data of arbitrary size to fixed-size values using a hash function. Hash tables (also called hash maps) use this technique to implement associative arrays, enabling average O(1) time complexity for insert, delete, and search operations. This makes hashing one of the most important data structures for efficient data retrieval.

**Why Hashing Exists:**
- Arrays provide O(1) access by index but not by key
- Linked lists provide O(n) search by key
- Binary search trees provide O(log n) search but require ordering
- Hash tables provide O(1) average search by key
- Essential for fast lookups in large datasets

**Where It Is Used:**
- Database indexing and caching
- Session management and authentication
- Deduplication and duplicate detection
- Frequency counting and analytics
- Symbol tables in compilers
- Spell checkers and dictionaries
- Load balancing (consistent hashing)
- Cryptographic applications

## Core Concept Explanation

Hashing works by applying a hash function to a key to compute an index in an array (the hash table). The key-value pair is stored at this index. When multiple keys hash to the same index, a collision occurs, which must be resolved using techniques like chaining or open addressing.

**Step-by-Step Breakdown:**
1. Apply hash function to key to get index
2. Check if index is occupied
3. If empty: store key-value pair
4. If occupied: handle collision (chaining or probing)
5. For lookup: hash key, check index, handle collisions
6. For delete: hash key, find and remove entry

**Intuition Behind the Concept:**
Think of a library with numbered shelves. When you get a book, you compute its shelf number based on the book's title (hash function). If the shelf is full, you put the book on an overflow shelf (chaining) or find the next empty shelf (open addressing). To find a book later, you compute the shelf number and look there.

**Visual Thinking:**
```
Hash Table with Chaining:
Index 0: [key1, value1] -> [key4, value4] -> null
Index 1: [key2, value2] -> null
Index 2: null
Index 3: [key3, value3] -> [key5, value5] -> null
Index 4: null

Hash Function: hash(key) = key % 5
key1 = 11 → 11 % 5 = 1 → Index 1
key2 = 23 → 23 % 5 = 3 → Index 3
key3 = 18 → 18 % 5 = 3 → Index 3 (collision with key2)
key4 = 6  → 6 % 5 = 1 → Index 1 (collision with key1)
key5 = 28 → 28 % 5 = 3 → Index 3 (collision with key2, key3)
```

## Internal Working / Logic

Hash tables operate through two primary components: the hash function and collision resolution strategy.

**Component 1: Hash Function**
- Converts key to array index
- Should distribute keys uniformly
- Should be fast to compute
- Should minimize collisions

**Component 2: Collision Resolution**

**Chaining (Separate Chaining):**
- Each bucket holds a linked list of entries
- Simple to implement
- Handles any number of collisions
- Memory overhead for pointers

**Open Addressing:**
- Find next empty slot using probing
- Linear probing: check next slot
- Quadratic probing: check slots with quadratic intervals
- Double hashing: use second hash function
- Better cache locality
- Limited by table size

**Flow Explanation (Insert with Chaining):**
1. Compute hash(key) to get index
2. Access bucket at index
3. If bucket empty: create new entry
4. If bucket occupied: traverse linked list
5. If key found: update value
6. If key not found: add to end of list
7. Return

**Flow Explanation (Lookup with Chaining):**
1. Compute hash(key) to get index
2. Access bucket at index
3. Traverse linked list
4. If key found: return value
5. If key not found: return not found
6. Return

**Decision Making Logic:**
The key decision is which collision resolution strategy to use:
- Chaining: simpler, handles many collisions, more memory
- Open addressing: better cache locality, limited capacity, complex
- Choice depends on expected load factor and memory constraints

## Algorithm / Approach

**Insert Algorithm (Chaining)**

```
1. Compute index = hash(key)
2. If bucket at index is empty:
   a. Create new entry with key-value
   b. Store at bucket
3. Else:
   a. Traverse linked list at bucket
   b. If key found: update value
   c. Else: add new entry to end
4. Return
```

**Lookup Algorithm (Chaining)**

```
1. Compute index = hash(key)
2. If bucket at index is empty: return not found
3. Traverse linked list at bucket
4. If key found: return value
5. Return not found
```

**Delete Algorithm (Chaining)**

```
1. Compute index = hash(key)
2. If bucket at index is empty: return
3. Traverse linked list at bucket
4. If key found: remove entry
5. Return
```

**Hash Function Design**

```
1. Consider key type (integer, string, object)
2. Choose appropriate hash algorithm
3. Ensure uniform distribution
4. Minimize collisions
5. Compute efficiently
```

## Implementations

### 1. Counting Frequencies

```javascript
function countFrequencies(arr) {
  const freq = new Map();
  
  for (const num of arr) {
    freq.set(num, (freq.get(num) || 0) + 1);
  }
  
  return freq;
}
```

**Advantages:**
- O(n) time, O(n) space
- Single pass through array
- Handles any data type

### 2. Two Sum

```javascript
function twoSum(nums, target) {
  const seen = new Map();
  
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    
    if (seen.has(complement)) {
      return [seen.get(complement), i];
    }
    
    seen.set(nums[i], i);
  }
  
  return [];
}
```

**Advantages:**
- O(n) time, O(n) space
- Single pass through array
- No sorting required

### 3. Subarray Sum Equals K

```javascript
function subarraySum(arr, k) {
  let prefixSum = 0;
  const sumMap = new Map([[0, -1]]);
  let count = 0;
  
  for (let i = 0; i < arr.length; i++) {
    prefixSum += arr[i];
    
    if (sumMap.has(prefixSum - k)) {
      count += sumMap.get(prefixSum - k);
    }
    
    sumMap.set(prefixSum, (sumMap.get(prefixSum) || 0) + 1);
  }
  
  return count;
}
```

**State Definition:**
- Track prefix sum at each index
- Use hash map to store prefix sum frequencies
- If (prefixSum - k) exists, subarray with sum k exists

### 4. Group Anagrams

```javascript
function groupAnagrams(strs) {
  const map = new Map();
  
  for (const str of strs) {
    const key = str.split('').sort().join('');
    
    if (!map.has(key)) {
      map.set(key, []);
    }
    
    map.get(key).push(str);
  }
  
  return Array.from(map.values());
}
```

**Advantages:**
- O(n * k log k) time (k = avg string length)
- O(n * k) space
- Groups anagrams efficiently

### 5. Longest Consecutive Sequence

```javascript
function longestConsecutive(nums) {
  const numSet = new Set(nums);
  let longest = 0;
  
  for (const num of numSet) {
    // Only start from beginning of sequence
    if (!numSet.has(num - 1)) {
      let current = num;
      let streak = 1;
      
      while (numSet.has(current + 1)) {
        current++;
        streak++;
      }
      
      longest = Math.max(longest, streak);
    }
  }
  
  return longest;
}
```

**Advantages:**
- O(n) time, O(n) space
- No sorting required
- Handles duplicates with Set

### 6. First Unique Character in String

```javascript
function firstUniqChar(s) {
  const freq = new Map();
  
  // Count frequencies
  for (const char of s) {
    freq.set(char, (freq.get(char) || 0) + 1);
  }
  
  // Find first unique
  for (let i = 0; i < s.length; i++) {
    if (freq.get(s[i]) === 1) {
      return i;
    }
  }
  
  return -1;
}
```

## Dry Run

**Example: Two Sum**

**Input:**
```
nums = [2, 7, 11, 15]
target = 9
```

**Step-by-Step Execution:**

```
Initial State:
seen = Map {}

Iteration 1 (i = 0):
nums[0] = 2
complement = 9 - 2 = 7
seen.has(7) = false
seen.set(2, 0)
seen = Map {2: 0}

Iteration 2 (i = 1):
nums[1] = 7
complement = 9 - 7 = 2
seen.has(2) = true
Return [seen.get(2), 1] = [0, 1]
```

**Variable Changes Table:**

| Iteration | i | nums[i] | complement | seen.has(complement) | seen (after) | Action |
|-----------|---|---------|------------|---------------------|--------------|--------|
| 1 | 0 | 2 | 7 | false | `{2: 0}` | Insert 2 |
| 2 | 1 | 7 | 2 | true | `{2: 0}` | Return `[0,1]` |

## Edge Cases

### 1. Empty Array
```javascript
nums = [], target = 9
Loop doesn't execute
Return []
```

### 2. No Solution
```javascript
nums = [1, 2, 3], target = 100
Loop completes without finding complement
Return []
```

### 3. Duplicate Elements
```javascript
nums = [3, 3], target = 6
First 3: complement = 3, not in map, insert
Second 3: complement = 3, in map, return [0, 1]
```

### 4. Negative Numbers
```javascript
nums = [-3, 4, 3], target = 0
complement = 0 - (-3) = 3
Works correctly with negatives
```

### 5. Single Element
```javascript
nums = [5], target = 10
complement = 5, not in map
Return []
```

### 6. Hash Collisions
```javascript
Multiple keys hash to same index
Handled by collision resolution
Affects performance but not correctness
```

**Why Edge Cases Matter:**
- Empty inputs prevent errors
- No solution cases must return appropriate values
- Duplicates test correctness
- Negative numbers test algorithm robustness
- Collisions test collision resolution

## Variations / Extensions

### 1. LRU Cache

```javascript
class LRUCache {
  constructor(capacity) {
    this.capacity = capacity;
    this.cache = new Map();
  }
  
  get(key) {
    if (!this.cache.has(key)) return -1;
    
    const value = this.cache.get(key);
    this.cache.delete(key);
    this.cache.set(key, value);
    
    return value;
  }
  
  put(key, value) {
    if (this.cache.has(key)) {
      this.cache.delete(key);
    }
    
    this.cache.set(key, value);
    
    if (this.cache.size > this.capacity) {
      const firstKey = this.cache.keys().next().value;
      this.cache.delete(firstKey);
    }
  }
}
```

### 2. Consistent Hashing

```javascript
class ConsistentHash {
  constructor() {
    this.ring = new Map();
    this.virtualNodes = 3;
  }
  
  addServer(server) {
    for (let i = 0; i < this.virtualNodes; i++) {
      const key = `${server}:${i}`;
      const hash = this._hash(key);
      this.ring.set(hash, server);
    }
  }
  
  removeServer(server) {
    for (let i = 0; i < this.virtualNodes; i++) {
      const key = `${server}:${i}`;
      const hash = this._hash(key);
      this.ring.delete(hash);
    }
  }
  
  getServer(key) {
    const hash = this._hash(key);
    const hashes = Array.from(this.ring.keys()).sort((a, b) => a - b);
    
    for (const h of hashes) {
      if (h >= hash) return this.ring.get(h);
    }
    
    return this.ring.get(hashes[0]);
  }
  
  _hash(key) {
    let hash = 0;
    for (const char of key) {
      hash = (hash * 31 + char.charCodeAt(0)) % 360;
    }
    return hash;
  }
}
```

### 3. Bloom Filter

```javascript
class BloomFilter {
  constructor(size, hashCount) {
    this.size = size;
    this.hashCount = hashCount;
    this.bitArray = new Array(size).fill(false);
  }
  
  add(item) {
    for (let i = 0; i < this.hashCount; i++) {
      const hash = this._hash(item, i);
      this.bitArray[hash % this.size] = true;
    }
  }
  
  mightContain(item) {
    for (let i = 0; i < this.hashCount; i++) {
      const hash = this._hash(item, i);
      if (!this.bitArray[hash % this.size]) {
        return false;
      }
    }
    return true;
  }
  
  _hash(item, seed) {
    let hash = 0;
    const str = item.toString();
    for (let i = 0; i < str.length; i++) {
      hash = (hash * 31 + str.charCodeAt(i) + seed) % this.size;
    }
    return hash;
  }
}
```

### 4. Hash Set Implementation

```javascript
class HashSet {
  constructor() {
    this.buckets = new Array(16).fill(null).map(() => []);
    this.size = 0;
  }
  
  _hash(key) {
    let hash = 0;
    const str = key.toString();
    for (let i = 0; i < str.length; i++) {
      hash = (hash * 31 + str.charCodeAt(i)) % this.buckets.length;
    }
    return hash;
  }
  
  add(key) {
    const index = this._hash(key);
    const bucket = this.buckets[index];
    
    for (const item of bucket) {
      if (item === key) return false;
    }
    
    bucket.push(key);
    this.size++;
    
    if (this.size / this.buckets.length > 0.75) {
      this._resize();
    }
    
    return true;
  }
  
  has(key) {
    const index = this._hash(key);
    const bucket = this.buckets[index];
    
    for (const item of bucket) {
      if (item === key) return true;
    }
    
    return false;
  }
  
  _resize() {
    const oldBuckets = this.buckets;
    this.buckets = new Array(this.buckets.length * 2).fill(null).map(() => []);
    this.size = 0;
    
    for (const bucket of oldBuckets) {
      for (const item of bucket) {
        this.add(item);
      }
    }
  }
}
```

### 5. Hash Map with Custom Objects

```javascript
class HashMap {
  constructor() {
    this.buckets = new Array(16).fill(null).map(() => []);
  }
  
  _hash(key) {
    if (typeof key === 'object' && key !== null) {
      return this._hashObject(key);
    }
    return this._hashPrimitive(key);
  }
  
  _hashPrimitive(key) {
    let hash = 0;
    const str = key.toString();
    for (let i = 0; i < str.length; i++) {
      hash = (hash * 31 + str.charCodeAt(i)) % this.buckets.length;
    }
    return hash;
  }
  
  _hashObject(obj) {
    let hash = 0;
    const keys = Object.keys(obj).sort();
    for (const key of keys) {
      hash = (hash * 31 + this._hashPrimitive(key) + this._hashPrimitive(obj[key])) % this.buckets.length;
    }
    return hash;
  }
  
  set(key, value) {
    const index = this._hash(key);
    const bucket = this.buckets[index];
    
    for (const entry of bucket) {
      if (this._equal(entry.key, key)) {
        entry.value = value;
        return;
      }
    }
    
    bucket.push({ key, value });
  }
  
  get(key) {
    const index = this._hash(key);
    const bucket = this.buckets[index];
    
    for (const entry of bucket) {
      if (this._equal(entry.key, key)) {
        return entry.value;
      }
    }
    
    return undefined;
  }
  
  _equal(a, b) {
    if (a === b) return true;
    if (typeof a !== typeof b) return false;
    if (typeof a === 'object') {
      return JSON.stringify(a) === JSON.stringify(b);
    }
    return false;
  }
}
```

## Optimization Techniques

### 1. Load Factor Management

**Dynamic Resizing:**
```javascript
// Resize when load factor > threshold
if (this.size / this.capacity > 0.75) {
  this._resize();
}
```

### 2. Better Hash Functions

**MurmurHash / FNV:**
```javascript
// Use well-known hash functions
// Better distribution than simple modulo
// Reduces collisions
```

### 3. Caching Hash Values

**Memoization:**
```javascript
// Cache hash values for immutable keys
// Avoid recomputing hash for same key
// Improves performance for repeated lookups
```

### 4. Trade-offs

**Hash Table vs Other Structures:**

| Aspect | Hash Table | Binary Search Tree | Sorted Array |
|--------|------------|-------------------|--------------|
| Search | `O(1)` avg | `O(log n)` | `O(log n)` |
| Insert | `O(1)` avg | `O(log n)` | `O(n)` |
| Delete | `O(1)` avg | `O(log n)` | `O(n)` |
| Order | No | Yes | Yes |
| Space | `O(n)` | `O(n)` | `O(n)` |
| Best For | Fast lookups | Ordered data | Static data |

**When to Use BST Instead:**
- Need ordered traversal
- Need range queries
- Need minimum/maximum operations
- Need predecessor/successor

## Complexity Analysis

### Time Complexity

**Average Case: O(1)**
- Hash function: O(1)
- Collision resolution: O(1) with good hash
- Insert, delete, search: O(1) average

**Worst Case: O(n)**
- All keys hash to same index
- Degenerates to linked list
- Insert, delete, search: O(n)

**With Resizing: Amortized O(1)**
- Resizing is O(n) but rare
- Amortized over many operations: O(1)
- Similar to dynamic array resizing

### Space Complexity

**Storage: O(n)**
- Store n key-value pairs
- Additional space for collision resolution
- Chaining: O(n) for linked list nodes
- Open addressing: O(n) for table

**Load Factor:**
- Ratio of elements to table size
- Optimal: 0.7 - 0.75
- Higher: more collisions, slower
- Lower: wasted space

**Explanation:**
Hash tables achieve O(1) average time through good hash functions and collision resolution. Worst case is O(n) but rare with good design. Space is O(n) with overhead for collision handling.

## Real-world Applications

### 1. Database Indexing

**Hash Indexes:**
- Fast equality lookups
- Used in databases for primary keys
- Example: MongoDB hash indexes

### 2. Caching Layers

**Memory Cache:**
- Store frequently accessed data
- Fast lookups by key
- Example: Redis, Memcached

### 3. Session Management

**User Sessions:**
- Store session data by session ID
- Fast retrieval
- Example: Web application sessions

### 4. Deduplication

**Duplicate Detection:**
- Track seen items
- Filter duplicates
- Example: Data pipelines, ETL

### 5. Load Balancing

**Consistent Hashing:**
- Distribute requests across servers
- Handle server additions/removals
- Example: CDN, distributed caches

### 6. Symbol Tables

**Compiler Design:**
- Track variables and functions
- Fast lookups during compilation
- Example: Programming language compilers

### 7. Spell Checkers

**Dictionary Lookup:**
- Check if word exists
- Fast dictionary access
- Example: Word processors

### 8. Cryptographic Applications

**Digital Signatures:**
- Hash data for signatures
- Verify integrity
- Example: SSL/TLS, blockchain

## Common Mistakes

### 1. Poor Hash Function

**Mistake:**
```javascript
// Bad hash function
function hash(key) {
  return key % 10; // Only 10 buckets!
}
```

**Correct:**
```javascript
// Better hash function
function hash(key) {
  let hash = 0;
  const str = key.toString();
  for (let i = 0; i < str.length; i++) {
    hash = (hash * 31 + str.charCodeAt(i)) % 1000;
  }
  return hash;
}
```

**Why It Matters:**
- Poor distribution causes many collisions
- Degrades to O(n) performance
- Must use good hash function

### 2. Not Handling Collisions

**Mistake:**
```javascript
// No collision handling
table[hash(key)] = value; // Overwrites!
```

**Correct:**
```javascript
// Handle collisions
if (table[hash(key)]) {
  // Use chaining or probing
}
```

**Why It Matters:**
- Collisions are inevitable
- Must handle them correctly
- Otherwise data is lost

### 3. Not Resizing

**Mistake:**
```javascript
// Fixed size table
const table = new Array(100); // Never resizes
```

**Correct:**
```javascript
// Dynamic resizing
if (size / capacity > 0.75) {
  resize();
}
```

**Why It Matters:**
- Fixed size fills up
- Performance degrades
- Must resize to maintain O(1)

### 4. Using Wrong Data Structure

**Mistake:**
```javascript
// Using hash map when order matters
const map = new Map();
// Need to iterate in insertion order
```

**Correct:**
```javascript
// Use LinkedHashMap or tree map
// If order matters
```

**Why It Matters:**
- Hash maps don't maintain order
- Wrong choice leads to bugs
- Must use appropriate structure

### 5. Not Checking for Null

**Mistake:**
```javascript
// Not checking for null/undefined
const value = map.get(key);
value.toString(); // May crash
```

**Correct:**
```javascript
// Check before using
const value = map.get(key);
if (value !== undefined) {
  value.toString();
}
```

**Why It Matters:**
- get() returns undefined for missing keys
- Must check before using
- Prevents runtime errors

### 6. Mutable Keys

**Mistake:**
```javascript
// Using mutable objects as keys
const key = { id: 1 };
map.set(key, value);
key.id = 2; // Key changed!
map.get(key); // Won't find it
```

**Correct:**
```javascript
// Use immutable keys
const key = { id: 1 };
Object.freeze(key);
map.set(key, value);
```

**Why It Matters:**
- Mutable keys break hash maps
- Hash changes after insertion
- Can't retrieve value later

## Advanced Concepts

### 1. Robin Hood Hashing

**Concept:**
Move elements closer to their ideal position to reduce probe length.

**Features:**
- Reduces variance in probe length
- Better cache locality
- More complex implementation

### 2. Cuckoo Hashing

**Concept:**
Use multiple hash functions and relocate elements on collision.

**Features:**
- Worst-case O(1) lookup
- Multiple hash tables
- Good for read-heavy workloads

### 3. Hopscotch Hashing

**Concept:**
Constrain where elements can be placed to improve locality.

**Features:**
- Good cache performance
- Bounded probe length
- Complex implementation

### 4. Linear Hashing

**Concept:**
Dynamic hashing scheme that grows table incrementally.

**Features:**
- No global rehashing
- Gradual expansion
- Good for large datasets

## Practice Thinking Guide

### How to Identify When to Use Hashing

**Key Signals in Problem Statements:**

1. **"Find if element exists"**
   - Use hash set for existence check
   - Example: "Contains duplicate"

2. **"Count frequency of elements"**
   - Use hash map for counting
   - Example: "Top K frequent elements"

3. **"Find pair/triplet with sum X"**
   - Use hash map for complement lookup
   - Example: "Two sum"

4. **"Group by some property"**
   - Use hash map with property as key
   - Example: "Group anagrams"

5. **"Subarray with sum X"**
   - Use hash map with prefix sums
   - Example: "Subarray sum equals K"

6. **"First unique/repeated element"**
   - Use hash map/set for tracking
   - Example: "First unique character"

**Pattern Recognition:**

**Pattern 1: Existence Check**
```
Problem: Check if element exists
Solution: Hash set
```

**Pattern 2: Frequency Counting**
```
Problem: Count occurrences
Solution: Hash map with counts
```

**Pattern 3: Complement Lookup**
```
Problem: Find pair with property
Solution: Hash map for complements
```

**Pattern 4: Grouping**
```
Problem: Group by property
Solution: Hash map with property key
```

**Pattern 5: Prefix Sum**
```
Problem: Subarray with sum X
Solution: Hash map with prefix sums
```

**Decision Flowchart:**

```
Need fast lookup by key?
├─ Yes → Need to count frequencies?
│        ├─ Yes → Use hash map
│        └─ No → Use hash set
├─ No → Need to find pairs/triplets?
│        ├─ Yes → Use hash map for complements
│        └─ No → Consider other approach
└─ No → Not hashing problem
```

**Example Problem Analysis:**

**Problem:** "Find two numbers that sum to target"

**Analysis:**
1. Need to find pair with sum X
2. For each number, need to find complement
3. Hash map provides O(1) complement lookup
4. Store seen numbers in hash map
5. Solution: Hash map with complement check

**Problem:** "Group anagrams together"

**Analysis:**
1. Need to group strings by anagram property
2. Anagrams have same sorted characters
3. Use sorted string as hash key
4. Group strings with same key
5. Solution: Hash map with sorted key

**Problem:** "Count subarrays with sum K"

**Analysis:**
1. Need to find subarrays with specific sum
2. Use prefix sum technique
3. If (prefixSum - K) exists, subarray exists
4. Track prefix sum frequencies
5. Solution: Hash map with prefix sums

## Summary

Hashing is a fundamental technique that enables O(1) average time complexity for insert, delete, and search operations. It's essential for fast lookups, frequency counting, and many other applications. Understanding hash functions, collision resolution, and trade-offs is crucial for effective use.

**Key Takeaways:**
- O(1) average, O(n) worst case time complexity
- Requires good hash function for uniform distribution
- Collision resolution: chaining or open addressing
- Monitor load factor and resize when needed
- Use built-in hash maps when available
- Not suitable for ordered operations
- Handle edge cases (empty, no solution, duplicates)

**Mastery Checklist:**
- ✅ Understand hash function design
- ✅ Implement collision resolution
- ✅ Solve two-sum with hash map
- ✅ Count frequencies efficiently
- ✅ Group by properties
- ✅ Use prefix sum technique
- ✅ Handle resizing and load factor
- ✅ Choose appropriate data structure

