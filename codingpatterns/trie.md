# Trie (Prefix Tree)

Trie (prefix tree) is a tree-like data structure used to store strings where each node represents a character. It enables efficient prefix-based searches.

## Introduction

Trie (pronounced "try") is a tree-like data structure used for storing strings where each node represents a character. Unlike hash tables, which provide O(1) average time for exact matches but don't support prefix searches efficiently, tries provide O(m) time for insert, search, and prefix operations where m is the string length. Tries are particularly useful for applications that require prefix-based searches, autocomplete systems, spell checkers, and dictionary implementations.

**Why Tries Exist:**
- Hash tables don't support prefix searches efficiently
- Binary search trees can't handle prefix operations naturally
- Tries provide O(m) time for all operations
- No hash collisions to worry about
- Natural for string-based operations
- Efficient for autocomplete and suggestions

**Where It Is Used:**
- Autocomplete systems (Google search, IDE suggestions)
- Spell checkers and dictionaries
- IP routing tables (longest prefix matching)
- Text prediction and auto-correction
- Contact search in phones
- DNA sequence analysis
- Word games and puzzles
- Search engine indexing

## Core Concept Explanation

A trie is a tree where each node represents a character. The root represents an empty string, and each path from the root to a node represents a prefix. Words are stored by traversing the trie character by character, creating new nodes as needed. Each node may have a flag indicating whether it marks the end of a word. This structure enables efficient prefix searches because all words sharing a prefix share the same path in the trie.

**Step-by-Step Breakdown:**
1. Start at the root node (represents empty string)
2. For each character in the string:
   - Check if child node exists for that character
   - If not, create a new child node
   - Move to the child node
3. Mark the final node as end of word
4. For search, traverse the trie character by character
5. For prefix search, check if path exists
6. For autocomplete, collect all words from prefix node

**Intuition Behind the Concept:**
Think of a trie like a dictionary's index. In a physical dictionary, you can quickly find all words starting with "app" by going to the "A" section, then "ap", then "app". A trie structures data the same way - all words sharing a prefix share the same path, making prefix operations extremely efficient.

**Visual Thinking:**
```
Trie Structure for ["app", "apple", "application", "bat", "ball"]

          root
         /  \
        a    b
       /      \
      p        a
     / \        \
    p   p        t
   /     \        \
  l      p        l
 /       / \        \
e       l   i        l
            / \
           c   o
          /     \
         a       n
        /         \
       t          s
      /
     i
    /
   o
   /
  n

Words:
- app (root → a → p → p ✓)
- apple (root → a → p → p → l → e ✓)
- application (root → a → p → p → l → i → c → a → t → i → o → n ✓)
- bat (root → b → a → t ✓)
- ball (root → b → a → l → l ✓)
```

## Internal Working / Logic

Tries operate through a tree structure where each node contains a map of child nodes (character to node) and a flag indicating if it's the end of a word. The key operations are insert, search, and prefix search, all of which traverse the trie character by character.

**Operation 1: Insert**
- Start at the root node
- For each character in the word:
  - Check if child node exists for that character
  - If not, create a new child node
  - Move to the child node
- Mark the final node as end of word

**Operation 2: Search**
- Start at the root node
- For each character in the word:
  - Check if child node exists for that character
  - If not, return false
  - Move to the child node
- Return true if final node is marked as end of word

**Operation 3: Prefix Search**
- Start at the root node
- For each character in the prefix:
  - Check if child node exists for that character
  - If not, return false
  - Move to the child node
- Return true (path exists)

**Operation 4: Autocomplete**
- Perform prefix search to find prefix node
- If prefix doesn't exist, return empty
- From prefix node, perform DFS to collect all words
- Return collected words

**Flow Explanation (Insert "apple"):**
1. Start at root
2. Check if 'a' child exists - no, create it
3. Move to 'a' node
4. Check if 'p' child exists - no, create it
5. Move to 'p' node
6. Check if 'p' child exists - no, create it
7. Move to 'p' node
8. Check if 'l' child exists - no, create it
9. Move to 'l' node
10. Check if 'e' child exists - no, create it
11. Move to 'e' node
12. Mark 'e' node as end of word

**Decision Making Logic:**
The key decision is how to store children:
- Use hash map (object) for O(1) child lookup
- Use array for fixed character set (ASCII)
- Use linked list for memory efficiency
- Hash map is most common for flexibility

## Algorithm / Approach

**Insert Algorithm**

```
1. Start at root node
2. For each character in word:
   a. If child node doesn't exist, create it
   b. Move to child node
3. Mark final node as end of word
```

**Search Algorithm**

```
1. Start at root node
2. For each character in word:
   a. If child node doesn't exist, return false
   b. Move to child node
3. Return true if final node is end of word
```

**Prefix Search Algorithm**

```
1. Start at root node
2. For each character in prefix:
   a. If child node doesn't exist, return false
   b. Move to child node
3. Return true (path exists)
```

**Autocomplete Algorithm**

```
1. Perform prefix search to find prefix node
2. If prefix doesn't exist, return empty
3. From prefix node, perform DFS:
   a. If node is end of word, add to results
   b. For each child, recursively search
4. Return collected words
```

## Implementations

### 1. Basic Trie

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }
  
  insert(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
    }
    node.isEnd = true;
  }
  
  search(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return node.isEnd;
  }
  
  startsWith(prefix) {
    let node = this.root;
    for (const char of prefix) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return true;
  }
}
```

**Advantages:**
- O(m) time for all operations
- Simple and intuitive
- Flexible character set
- No hash collisions

### 2. Trie with Autocomplete

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }
  
  insert(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
    }
    node.isEnd = true;
  }
  
  search(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return node.isEnd;
  }
  
  startsWith(prefix) {
    let node = this.root;
    for (const char of prefix) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return true;
  }
  
  autocomplete(prefix) {
    let node = this.root;
    for (const char of prefix) {
      if (!node.children[char]) {
        return [];
      }
      node = node.children[char];
    }
    
    const results = [];
    this._dfs(node, prefix, results);
    return results;
  }
  
  _dfs(node, current, results) {
    if (node.isEnd) {
      results.push(current);
    }
    
    for (const char in node.children) {
      this._dfs(node.children[char], current + char, results);
    }
  }
}
```

**Advantages:**
- Supports autocomplete
- DFS for word collection
- Efficient prefix-based search

### 3. Trie with Deletion

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }
  
  insert(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) {
        node.children[char] = new TrieNode();
      }
      node = node.children[char];
    }
    node.isEnd = true;
  }
  
  search(word) {
    let node = this.root;
    for (const char of word) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return node.isEnd;
  }
  
  startsWith(prefix) {
    let node = this.root;
    for (const char of prefix) {
      if (!node.children[char]) {
        return false;
      }
      node = node.children[char];
    }
    return true;
  }
  
  delete(word) {
    return this._delete(this.root, word, 0);
  }
  
  _delete(node, word, index) {
    if (index === word.length) {
      if (!node.isEnd) {
        return false;
      }
      node.isEnd = false;
      return Object.keys(node.children).length === 0;
    }
    
    const char = word[index];
    if (!node.children[char]) {
      return false;
    }
    
    const shouldDelete = this._delete(node.children[char], word, index + 1);
    
    if (shouldDelete) {
      delete node.children[char];
      return Object.keys(node.children).length === 0 && !node.isEnd;
    }
    
    return false;
  }
}
```

**Advantages:**
- Supports deletion
- Removes unused nodes
- Memory efficient

## Dry Run

**Example: Insert ["app", "apple", "application"]**

**Input:**
```
words = ["app", "apple", "application"]
```

**Step-by-Step Execution:**

```
Initial State:
root = {children: {}, isEnd: false}

Insert "app":
Step 1: char = 'a'
  root.children['a'] doesn't exist, create node
  node = root.children['a']
  
Step 2: char = 'p'
  node.children['p'] doesn't exist, create node
  node = node.children['p']
  
Step 3: char = 'p'
  node.children['p'] doesn't exist, create node
  node = node.children['p']
  
Step 4: Mark node.isEnd = true

Trie after "app":
root
 └─ a
    └─ p
       └─ p (isEnd: true)

Insert "apple":
Step 1: char = 'a'
  root.children['a'] exists
  node = root.children['a']
  
Step 2: char = 'p'
  node.children['p'] exists
  node = node.children['p']
  
Step 3: char = 'p'
  node.children['p'] exists
  node = node.children['p']
  
Step 4: char = 'l'
  node.children['l'] doesn't exist, create node
  node = node.children['l']
  
Step 5: char = 'e'
  node.children['e'] doesn't exist, create node
  node = node.children['e']
  
Step 6: Mark node.isEnd = true

Trie after "apple":
root
 └─ a
    └─ p
       └─ p (isEnd: true)
          └─ l
             └─ e (isEnd: true)

Insert "application":
Step 1: char = 'a'
  root.children['a'] exists
  node = root.children['a']
  
Step 2: char = 'p'
  node.children['p'] exists
  node = node.children['p']
  
Step 3: char = 'p'
  node.children['p'] exists
  node = node.children['p']
  
Step 4: char = 'l'
  node.children['l'] exists
  node = node.children['l']
  
Step 5: char = 'i'
  node.children['i'] doesn't exist, create node
  node = node.children['i']
  
Step 6: char = 'c'
  node.children['c'] doesn't exist, create node
  node = node.children['c']
  
Step 7: char = 'a'
  node.children['a'] doesn't exist, create node
  node = node.children['a']
  
Step 8: char = 't'
  node.children['t'] doesn't exist, create node
  node = node.children['t']
  
Step 9: char = 'i'
  node.children['i'] doesn't exist, create node
  node = node.children['i']
  
Step 10: char = 'o'
  node.children['o'] doesn't exist, create node
  node = node.children['o']
  
Step 11: char = 'n'
  node.children['n'] doesn't exist, create node
  node = node.children['n']
  
Step 12: Mark node.isEnd = true

Final Trie:
root
 └─ a
    └─ p
       └─ p (isEnd: true)
          ├─ l
          │  ├─ e (isEnd: true)
          │  └─ i
          │     └─ c
          │        └─ a
          │           └─ t
          │              └─ i
          │                 └─ o
          │                    └─ n (isEnd: true)
```

**Variable Changes Table:**

| Operation | Character | Action | Node Created | isEnd |
|-----------|-----------|--------|-------------|-------|
| Insert "app" | 'a' | Create child | root.children['a'] | false |
| Insert "app" | 'p' | Create child | a.children['p'] | false |
| Insert "app" | 'p' | Create child | p.children['p'] | true |
| Insert "apple" | 'a' | Move to existing | - | false |
| Insert "apple" | 'p' | Move to existing | - | false |
| Insert "apple" | 'p' | Move to existing | - | false |
| Insert "apple" | 'l' | Create child | p.children['l'] | false |
| Insert "apple" | 'e' | Create child | l.children['e'] | true |
| Insert "application" | 'a' | Move to existing | - | false |
| Insert "application" | 'p' | Move to existing | - | false |
| Insert "application" | 'p' | Move to existing | - | false |
| Insert "application" | 'l' | Move to existing | - | false |
| Insert "application" | 'i' | Create child | l.children['i'] | false |
| Insert "application" | 'c' | Create child | i.children['c'] | false |
| Insert "application" | 'a' | Create child | c.children['a'] | false |
| Insert "application" | 't' | Create child | a.children['t'] | false |
| Insert "application" | 'i' | Create child | t.children['i'] | false |
| Insert "application" | 'o' | Create child | i.children['o'] | false |
| Insert "application" | 'n' | Create child | o.children['n'] | true |

## Edge Cases

### 1. Empty String
```javascript
trie.insert("")
trie.search("") → true (if root marked as end)
Handle empty string specially
```

### 2. Duplicate Insert
```javascript
trie.insert("app")
trie.insert("app")
trie.search("app") → true
No error, just marks end again
```

### 3. Prefix of Another Word
```javascript
trie.insert("app")
trie.insert("apple")
trie.search("app") → true
trie.search("apple") → true
Both words exist
```

### 4. Non-existent Word
```javascript
trie.insert("app")
trie.search("apple") → false
Word not in trie
```

### 5. Case Sensitivity
```javascript
trie.insert("App")
trie.search("app") → false
Case-sensitive by default
```

### 6. Special Characters
```javascript
trie.insert("hello!")
trie.search("hello!") → true
Special characters handled
```

**Why Edge Cases Matter:**
- Empty string is valid word
- Duplicates should not cause errors
- Prefix relationships are common
- Case sensitivity affects results
- Special characters need handling

## Variations / Extensions

### 1. Compressed Trie (Radix Tree)

```javascript
class CompressedTrieNode {
  constructor(prefix = '') {
    this.prefix = prefix;
    this.children = {};
    this.isEnd = false;
  }
}
```

### 2. Suffix Trie

```javascript
// Build trie of all suffixes
// Useful for substring search
// Space: O(n²) for string of length n
```

### 3. Ternary Search Tree

```javascript
class TSTNode {
  constructor(char) {
    this.char = char;
    this.left = null;
    this.middle = null;
    this.right = null;
    this.isEnd = false;
  }
}
```

### 4. Trie with Frequency Count

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
    this.frequency = 0;
  }
}
```

### 5. Word Search II

```javascript
function findWords(board, words) {
  const trie = new Trie();
  for (const word of words) {
    trie.insert(word);
  }
  
  const result = new Set();
  const rows = board.length;
  const cols = board[0].length;
  
  function dfs(row, col, node, path) {
    const char = board[row][col];
    if (!node.children[char]) return;
    
    node = node.children[char];
    path += char;
    
    if (node.isEnd) {
      result.add(path);
    }
    
    board[row][col] = '#';
    
    const directions = [[0, 1], [1, 0], [0, -1], [-1, 0]];
    for (const [dr, dc] of directions) {
      const nr = row + dr;
      const nc = col + dc;
      if (nr >= 0 && nr < rows && nc >= 0 && nc < cols && board[nr][nc] !== '#') {
        dfs(nr, nc, node, path);
      }
    }
    
    board[row][col] = char;
  }
  
  for (let r = 0; r < rows; r++) {
    for (let c = 0; c < cols; c++) {
      dfs(r, c, trie.root, '');
    }
  }
  
  return Array.from(result);
}
```

## Optimization Techniques

### 1. Array for Children

**Fixed Character Set:**
```javascript
// Use array of size 26 for lowercase letters
// Faster lookup, more memory
// Good for known character sets
```

### 2. Compressed Nodes

**Merge Single Child:**
```javascript
// Merge nodes with single child
// Reduces memory usage
// Increases complexity
```

### 3. Lazy Deletion

**Mark as Deleted:**
```javascript
// Don't actually delete nodes
// Mark as deleted instead
// Reuse later if needed
```

### 4. Trade-offs

**Trie vs Hash Map:**

| Aspect | Trie | Hash Map |
|--------|------|----------|
| Insert | `O(m)` | `O(1)` average |
| Search | `O(m)` | `O(1)` average |
| Prefix Search | `O(m)` | `O(n)` |
| Space | `O(n*m)` | `O(n)` |
| Collisions | None | Possible |
| Best For | Prefix ops | Exact match |

**When to Use Trie:**
- Need prefix operations
- Many strings with common prefixes
- Autocomplete needed
- No hash collisions desired

## Complexity Analysis

### Time Complexity

**Insert: O(m)**
- m = length of word
- Create nodes as needed
- Example: insert("apple")

**Search: O(m)**
- m = length of word
- Traverse trie
- Example: search("apple")

**Prefix Search: O(m)**
- m = length of prefix
- Traverse trie
- Example: startsWith("app")

**Autocomplete: O(m + k)**
- m = length of prefix
- k = number of words with prefix
- DFS to collect words
- Example: autocomplete("app")

### Space Complexity

**Space: O(n * m)**
- n = number of words
- m = average word length
- Each character stored as node
- Shared prefixes reduce space

**Explanation:**
Trie space complexity is O(n * m) in the worst case (no shared prefixes). With shared prefixes, space is reduced. Each node stores a map of children and an end flag. The space can be optimized using arrays for fixed character sets or compressed tries.

## Real-world Applications

### 1. Autocomplete Systems

**Search Suggestions:**
- Google search autocomplete
- IDE code completion
- Browser URL suggestions
- Example: Type "app" → get suggestions

### 2. Spell Checkers

**Dictionary Lookup:**
- Word validation
- Spelling correction
- Document editors
- Example: Check if word exists

### 3. IP Routing

**Longest Prefix Match:**
- Router forwarding tables
- Network routing
- IP address lookup
- Example: Find route for IP

### 4. Contact Search

**Phone Contacts:**
- Contact name search
- Phone number lookup
- Email suggestions
- Example: Search contacts

### 5. Text Prediction

**Mobile Keyboards:**
- Next word prediction
- Auto-correction
- Emoji suggestions
- Example: Predict next word

### 6. DNA Analysis

**Bioinformatics:**
- DNA sequence matching
- Pattern search
- Genome analysis
- Example: Find DNA patterns

### 7. Word Games

**Games and Puzzles:**
- Scrabble word validation
- Crossword puzzles
- Word search
- Example: Validate words

### 8. Search Engines

**Indexing:**
- Inverted index
- Prefix-based search
- Query suggestions
- Example: Search engine autocomplete

## Common Mistakes

### 1. Not Marking End of Word

**Mistake:**
```javascript
// Not marking end of word
insert("app") // But don't mark isEnd
search("app") → false (wrong!)
```

**Correct:**
```javascript
// Always mark end of word
node.isEnd = true;
```

**Why It Matters:**
- Without marking, can't distinguish prefix from word
- "app" is a word, not just prefix of "apple"
- Critical for search correctness

### 2. Incorrect Child Creation

**Mistake:**
```javascript
// Not checking if child exists
node.children[char] = new TrieNode(); // Always create
```

**Correct:**
```javascript
// Check before creating
if (!node.children[char]) {
  node.children[char] = new TrieNode();
}
```

**Why It Matters:**
- Always creating wastes memory
- Overwrites existing nodes
- Breaks shared prefixes

### 3. Case Sensitivity

**Mistake:**
```javascript
// Not handling case
insert("App")
search("app") → false
```

**Correct:**
```javascript
// Normalize case
insert(word.toLowerCase())
search(word.toLowerCase())
```

**Why It Matters:**
- Case sensitivity affects results
- Users expect case-insensitive search
- Normalize input

### 4. Memory Inefficiency

**Mistake:**
```javascript
// Storing full strings at nodes
node.word = currentWord; // Wastes memory
```

**Correct:**
```javascript
// Only store end flag
node.isEnd = true;
```

**Why It Matters:**
- Storing strings wastes memory
- Trie already encodes path
- Use end flag instead

### 5. Not Handling Empty String

**Mistake:**
```javascript
// Not handling empty string
insert("") // May cause issues
```

**Correct:**
```javascript
// Handle empty string specially
if (word === "") {
  this.root.isEnd = true;
  return;
}
```

**Why It Matters:**
- Empty string is valid word
- Root represents empty string
- Handle edge case

### 6. Incorrect Deletion

**Mistake:**
```javascript
// Deleting nodes used by other words
delete node.children[char]; // May break other words
```

**Correct:**
```javascript
// Only delete if no other dependencies
if (Object.keys(node.children).length === 0 && !node.isEnd) {
  delete node.children[char];
}
```

**Why It Matters:**
- Deleting shared nodes breaks other words
- Must check dependencies
- Careful deletion needed

## Advanced Concepts

### 1. Compressed Trie

**Concept:**
Merge nodes with single child.

**Features:**
- Reduces memory usage
- Increases complexity
- Used in radix trees

### 2. Suffix Trie

**Concept:**
Trie of all suffixes of a string.

**Features:**
- Substring search
- Pattern matching
- Space: O(n²)

### 3. Ternary Search Tree

**Concept:**
Each node has three children.

**Features:**
- Space optimization
- Balanced structure
- Used in spell checkers

### 4. Aho-Corasick

**Concept:**
Multi-pattern matching automaton.

**Features:**
- Multiple pattern search
- Linear time
- Used in intrusion detection

## Practice Thinking Guide

### How to Identify When to Use Trie

**Key Signals in Problem Statements:**

1. **"Prefix" or "starts with"**
   - Prefix-based search
   - Example: "Autocomplete"

2. **"Dictionary" or "word list"**
   - String storage
   - Example: "Spell checker"

3. **"Multiple word search"**
   - Efficient lookup
   - Example: "Word search II"

4. **"Longest prefix match"**
   - IP routing
   - Example: "Routing table"

5. **"Suggestion" or "completion"**
   - Autocomplete
   - Example: "Search suggestions"

6. **"Pattern matching"**
   - String patterns
   - Example: "DNA analysis"

**Pattern Recognition:**

**Pattern 1: Autocomplete**
```
Problem: Provide suggestions as user types
Solution: Trie with prefix search + DFS
```

**Pattern 2: Spell Check**
```
Problem: Validate words
Solution: Trie with search
```

**Pattern 3: Word Search II**
```
Problem: Find all words in grid
Solution: Build trie, search grid
```

**Pattern 4: Replace Words**
```
Problem: Replace with shortest prefix
Solution: Trie of roots, find match
```

**Pattern 5: Longest Word**
```
Problem: Find longest word from letters
Solution: Trie with word building
```

**Decision Flowchart:**

```
Involves strings?
├─ Yes → Need prefix operations?
│        ├─ Yes → Use trie
│        └─ No → Use hash map
├─ No → Not trie problem
└─ No → Consider other
```

**Example Problem Analysis:**

**Problem:** "Implement autocomplete system"

**Analysis:**
1. Need to store words
2. Need to find words with prefix
3. Hash map can't do prefix search efficiently
4. Trie provides O(m) prefix search
5. Solution: Trie with autocomplete

**Problem:** "Word Search II - find all words in grid"

**Analysis:**
1. Need to search multiple words in grid
2. Brute force: search each word separately
3. Better: build trie of words, search grid once
4. Trie enables efficient matching
5. Solution: Build trie, DFS grid with trie

**Problem:** "Design add and search words with wildcard"

**Analysis:**
1. Need to support wildcard '.'
2. Regular trie search doesn't handle wildcard
3. Need to search all children for wildcard
4. Modified trie search with backtracking
5. Solution: Trie with wildcard search

## Summary

Trie is a tree-like data structure for storing strings where each node represents a character. It provides O(m) time for insert, search, and prefix operations, making it ideal for autocomplete, spell checkers, and dictionary implementations. Tries are particularly useful when prefix-based operations are needed, as they efficiently handle shared prefixes and enable fast prefix searches.

**Key Takeaways:**
- Trie stores strings in tree structure
- O(m) operations where m is string length
- Efficient for prefix-based searches
- Each node represents a character
- Mark end of word nodes
- No hash collisions
- Higher memory usage than hash map
- Essential for autocomplete systems

**Mastery Checklist:**
- ✅ Understand trie structure
- ✅ Implement insert operation
- ✅ Implement search operation
- ✅ Implement prefix search
- ✅ Implement autocomplete
- ✅ Handle edge cases
- ✅ Know when to use trie
- ✅ Understand complexity analysis
