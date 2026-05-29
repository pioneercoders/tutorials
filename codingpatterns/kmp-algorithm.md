# KMP Algorithm (Knuth-Morris-Pratt)

Knuth-Morris-Pratt (KMP) algorithm is a string matching algorithm that finds occurrences of a pattern in a text in linear time.

## Introduction

The Knuth-Morris-Pratt (KMP) algorithm is a string matching algorithm that finds all occurrences of a pattern string within a text string in linear time O(n + m), where n is the length of the text and m is the length of the pattern. Unlike naive string matching which has O(n * m) time complexity, KMP achieves linear time by preprocessing the pattern to create a Longest Prefix Suffix (LPS) array. This array allows the algorithm to skip unnecessary comparisons when a mismatch occurs, avoiding re-checking characters that are known to match. KMP is fundamental to text search, pattern matching, and is used in search engines, content filtering, and bioinformatics.

**Why KMP Exists:**
- Naive string matching is O(n * m)
- KMP achieves O(n + m) linear time
- Avoids re-checking known matches
- No backtracking in the text
- Efficient for large texts and patterns

**Where It Is Used:**
- Search engines (text indexing)
- Content filtering (pattern detection)
- Bioinformatics (DNA sequence matching)
- Text editors (find/replace)
- Log analysis (pattern search)
- Plagiarism detection
- Data validation (pattern matching)

## Core Concept Explanation

KMP algorithm works by preprocessing the pattern to create an LPS (Longest Prefix Suffix) array. For each position in the pattern, LPS[i] stores the length of the longest proper prefix that is also a suffix for the pattern[0..i]. This information allows us to skip characters when a mismatch occurs. When we have a mismatch at position j in the pattern, instead of starting over from the beginning, we use LPS[j-1] to determine how many characters we can skip. This is because the prefix of length LPS[j-1] is known to match, so we don't need to re-check those characters.

**Step-by-Step Breakdown:**
1. Build LPS array for the pattern
2. Start with i = 0 (text index) and j = 0 (pattern index)
3. Compare text[i] with pattern[j]
4. If match, increment both i and j
5. If mismatch and j > 0, set j = LPS[j-1]
6. If mismatch and j = 0, increment i
7. If j reaches pattern length, pattern found at i - j
8. Continue until end of text

**Intuition Behind the Concept:**
Think of KMP like reading a book with a bookmark. When you recognize a phrase you've seen before, you don't re-read it - you skip ahead. Similarly, when KMP finds a partial match and then a mismatch, it doesn't start over from the beginning. It uses the LPS array to know how much of the pattern is still valid and skips to the next possible match position. This is like knowing that "AB" matched, so if the next character doesn't match, you don't need to re-check "A" - you can skip to where "AB" could start again.

**Visual Thinking:**
```
Pattern: "ABABCABAB"
LPS Array: [0, 0, 1, 2, 0, 1, 2, 3, 4]

LPS Calculation:
- LPS[0] = 0 (single character, no proper prefix)
- LPS[1] = 0 ("AB" - no prefix = suffix)
- LPS[2] = 1 ("ABA" - "A" is prefix and suffix)
- LPS[3] = 2 ("ABAB" - "AB" is prefix and suffix)
- LPS[4] = 0 ("ABABC" - no prefix = suffix)
- LPS[5] = 1 ("ABABCA" - "A" is prefix and suffix)
- LPS[6] = 2 ("ABABCAB" - "AB" is prefix and suffix)
- LPS[7] = 3 ("ABABCABA" - "ABA" is prefix and suffix)
- LPS[8] = 4 ("ABABCABAB" - "ABAB" is prefix and suffix)

Text: "ABABDABACDABABCABAB"
Pattern: "ABABCABAB"

Matching Process:
Text:    A B A B D A B A C D A B A B C A B A B
Pattern: A B A B C A B A B
         ^ ^ ^ ^ X
         Match until 'D' != 'C'
         Use LPS[3] = 2, skip to position 2 in pattern
```

## Internal Working / Logic

KMP algorithm consists of two main phases: building the LPS array and searching for the pattern in the text. The LPS array is built by comparing the pattern with itself, finding the longest prefix that is also a suffix at each position. During the search phase, we use the LPS array to skip unnecessary comparisons when mismatches occur.

**Operation 1: Build LPS Array**
- Initialize LPS[0] = 0
- Use two pointers: length (for prefix) and i (for current position)
- If pattern[i] == pattern[length], increment both and set LPS[i] = length
- If mismatch and length > 0, set length = LPS[length - 1]
- If mismatch and length = 0, set LPS[i] = 0 and increment i
- Time: O(m), Space: O(m)

**Operation 2: Search Pattern in Text**
- Initialize i = 0 (text index) and j = 0 (pattern index)
- If text[i] == pattern[j], increment both
- If j reaches pattern length, pattern found at i - j
- If mismatch and j > 0, set j = LPS[j - 1]
- If mismatch and j = 0, increment i
- Continue until end of text
- Time: O(n), no backtracking in text

**Operation 3: Handle Multiple Matches**
- When pattern found, use LPS to find next possible match
- Set j = LPS[j - 1] to continue searching
- Allows finding all occurrences in single pass

**Flow Explanation (LPS Build):**
1. Initialize LPS[0] = 0, length = 0, i = 1
2. While i < pattern length:
   - If pattern[i] == pattern[length]:
     - Increment length, set LPS[i] = length, increment i
   - Else if length > 0:
     - Set length = LPS[length - 1]
   - Else:
     - Set LPS[i] = 0, increment i
3. Return LPS array

**Decision Making Logic:**
The key decisions are:
- When to skip characters (use LPS on mismatch)
- How much to skip (LPS[j-1] gives the skip amount)
- When pattern is found (j == pattern length)
- How to continue after finding pattern (use LPS to find next match)

## Algorithm / Approach

**Build LPS Array Algorithm**

```
1. Initialize LPS array of size m with zeros
2. Set length = 0, i = 1
3. While i < m:
   a. If pattern[i] == pattern[length]:
      i. Increment length
      ii. Set LPS[i] = length
      iii. Increment i
   b. Else if length > 0:
      i. Set length = LPS[length - 1]
   c. Else:
      i. Set LPS[i] = 0
      ii. Increment i
4. Return LPS array
```

**KMP Search Algorithm**

```
1. Build LPS array for pattern
2. Set i = 0 (text index), j = 0 (pattern index)
3. While i < n:
   a. If text[i] == pattern[j]:
      i. Increment i
      ii. Increment j
      iii. If j == m:
           - Pattern found at i - j
           - Set j = LPS[j - 1] to continue
   b. Else if j > 0:
      i. Set j = LPS[j - 1]
   c. Else:
      i. Increment i
4. Return all match positions
```

**Repeated Substring Pattern Algorithm**

```
1. Build LPS array for string
2. Let n = string length
3. If LPS[n-1] > 0 and n % (n - LPS[n-1]) == 0:
   - Return True (repeated pattern)
4. Return False
```

**Shortest Palindrome Algorithm**

```
1. Create new string = pattern + "#" + reverse(pattern)
2. Build LPS array for new string
3. The last value in LPS gives longest prefix-suffix match
4. Add reverse of remaining prefix to front
5. Return shortest palindrome
```

## Implementations

### 1. Basic KMP Search

```javascript
function buildLPS(pattern) {
  const lps = new Array(pattern.length).fill(0);
  let length = 0;
  let i = 1;
  
  while (i < pattern.length) {
    if (pattern[i] === pattern[length]) {
      length++;
      lps[i] = length;
      i++;
    } else {
      if (length !== 0) {
        length = lps[length - 1];
      } else {
        lps[i] = 0;
        i++;
      }
    }
  }
  
  return lps;
}

function kmpSearch(text, pattern) {
  if (!pattern) return 0;
  
  const lps = buildLPS(pattern);
  let i = 0, j = 0;
  const matches = [];
  
  while (i < text.length) {
    if (text[i] === pattern[j]) {
      i++;
      j++;
      
      if (j === pattern.length) {
        matches.push(i - j);
        j = lps[j - 1];
      }
    } else {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
  
  return matches;
}
```

**Advantages:**
- O(n + m) time complexity
- Finds all occurrences
- No backtracking in text

### 2. Implement strStr()

```javascript
function strStr(haystack, needle) {
  if (!needle) return 0;
  
  const lps = buildLPS(needle);
  let i = 0, j = 0;
  
  while (i < haystack.length) {
    if (haystack[i] === needle[j]) {
      i++;
      j++;
      
      if (j === needle.length) {
        return i - j;
      }
    } else {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
  
  return -1;
}
```

**Advantages:**
- Returns first occurrence
- Efficient for large texts
- Standard string search

### 3. Repeated Substring Pattern

```javascript
function repeatedSubstringPattern(s) {
  const lps = buildLPS(s);
  const n = s.length;
  
  if (lps[n - 1] > 0 && n % (n - lps[n - 1]) === 0) {
    return true;
  }
  return false;
}
```

**Advantages:**
- Detects repeated patterns
- Uses LPS property
- Efficient O(n) solution

### 4. Shortest Palindrome

```javascript
function shortestPalindrome(s) {
  if (!s) return "";
  
  const rev = s.split('').reverse().join('');
  const combined = s + "#" + rev;
  const lps = buildLPS(combined);
  
  const maxMatch = lps[lps.length - 1];
  const suffix = s.substring(maxMatch);
  
  return suffix.split('').reverse().join('') + s;
}
```

**Advantages:**
- Finds shortest palindrome
- Uses KMP for pattern matching
- Efficient solution

### 5. Count All Occurrences

```javascript
function countOccurrences(text, pattern) {
  if (!pattern) return 0;
  
  const lps = buildLPS(pattern);
  let i = 0, j = 0;
  let count = 0;
  
  while (i < text.length) {
    if (text[i] === pattern[j]) {
      i++;
      j++;
      
      if (j === pattern.length) {
        count++;
        j = lps[j - 1];
      }
    } else {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
  
  return count;
}
```

**Advantages:**
- Counts all pattern occurrences
- Single pass through text
- Efficient for counting

## Dry Run

**Example: KMP Search**

**Input:**
```
text = "ABABDABACDABABCABAB"
pattern = "ABABCABAB"
```

**Step-by-Step Execution:**

```
Build LPS for "ABABCABAB":
LPS = [0, 0, 1, 2, 0, 1, 2, 3, 4]

Search:
i=0, j=0: text[0]='A' == pattern[0]='A' → i=1, j=1
i=1, j=1: text[1]='B' == pattern[1]='B' → i=2, j=2
i=2, j=2: text[2]='A' == pattern[2]='A' → i=3, j=3
i=3, j=3: text[3]='B' == pattern[3]='B' → i=4, j=4
i=4, j=4: text[4]='D' != pattern[4]='C' → j = LPS[3] = 2
i=4, j=2: text[4]='D' != pattern[2]='A' → j = LPS[1] = 0
i=4, j=0: text[4]='D' != pattern[0]='A' → i=5
i=5, j=0: text[5]='A' == pattern[0]='A' → i=6, j=1
i=6, j=1: text[6]='B' == pattern[1]='B' → i=7, j=2
i=7, j=2: text[7]='A' == pattern[2]='A' → i=8, j=3
i=8, j=3: text[8]='C' == pattern[3]='B' → j = LPS[2] = 1
i=8, j=1: text[8]='C' != pattern[1]='B' → j = LPS[0] = 0
i=8, j=0: text[8]='C' != pattern[0]='A' → i=9
i=9, j=0: text[9]='D' != pattern[0]='A' → i=10
i=10, j=0: text[10]='A' == pattern[0]='A' → i=11, j=1
i=11, j=1: text[11]='B' == pattern[1]='B' → i=12, j=2
i=12, j=2: text[12]='A' == pattern[2]='A' → i=13, j=3
i=13, j=3: text[13]='B' == pattern[3]='B' → i=14, j=4
i=14, j=4: text[14]='C' == pattern[4]='C' → i=15, j=5
i=15, j=5: text[15]='A' == pattern[5]='A' → i=16, j=6
i=16, j=6: text[16]='B' == pattern[6]='B' → i=17, j=7
i=17, j=7: text[17]='A' == pattern[7]='A' → i=18, j=8
i=18, j=8: text[18]='B' == pattern[8]='B' → j=9 == pattern.length
Pattern found at i - j = 18 - 9 = 10
```

**Variable Changes Table:**

| i | j | text[i] | pattern[j] | Action | LPS Used |
|---|---|---------|------------|--------|----------|
| 0 | 0 | A | A | Match, i++, j++ | - |
| 1 | 1 | B | B | Match, i++, j++ | - |
| 2 | 2 | A | A | Match, i++, j++ | - |
| 3 | 3 | B | B | Match, i++, j++ | - |
| 4 | 4 | D | C | Mismatch, j = LPS[3] = 2 | 2 |
| 4 | 2 | D | A | Mismatch, j = LPS[1] = 0 | 0 |
| 4 | 0 | D | A | Mismatch, i++ | - |
| 5 | 0 | A | A | Match, i++, j++ | - |
| ... | ... | ... | ... | ... | ... |
| 10 | 0 | A | A | Match, i++, j++ | - |
| ... | ... | ... | ... | ... | ... |
| 18 | 8 | B | B | Match, j=9, FOUND | - |

## Edge Cases

### 1. Empty Pattern
```javascript
pattern = ""
kmpSearch(text, "") → 0 (or all positions)
Handle empty pattern
```

### 2. Pattern Longer Than Text
```javascript
text = "AB"
pattern = "ABC"
kmpSearch(text, pattern) → -1
No match possible
```

### 3. No Matches
```javascript
text = "ABCDEF"
pattern = "XYZ"
kmpSearch(text, pattern) → []
No occurrences
```

### 4. Single Character Pattern
```javascript
text = "ABABAB"
pattern = "A"
kmpSearch(text, pattern) → [0, 2, 4]
Multiple matches
```

### 5. Pattern at Beginning
```javascript
text = "ABCDEF"
pattern = "ABC"
kmpSearch(text, pattern) → [0]
Match at start
```

### 6. Pattern at End
```javascript
text = "ABCDEF"
pattern = "DEF"
kmpSearch(text, pattern) → [3]
Match at end
```

**Why Edge Cases Matter:**
- Empty pattern needs special handling
- Pattern longer than text can't match
- No matches should return empty array
- Single character pattern is valid
- Position of match matters
- Edge positions need correct handling

## Variations / Extensions

### 1. KMP with Wildcards

```javascript
function kmpWithWildcards(text, pattern) {
  const lps = buildLPSWithWildcards(pattern);
  let i = 0, j = 0;
  const matches = [];
  
  while (i < text.length) {
    if (pattern[j] === '?' || pattern[j] === text[i]) {
      i++;
      j++;
      
      if (j === pattern.length) {
        matches.push(i - j);
        j = lps[j - 1];
      }
    } else {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
  
  return matches;
}
```

### 2. Find All Occurrences

```javascript
function findAllOccurrences(text, pattern) {
  const lps = buildLPS(pattern);
  let i = 0, j = 0;
  const occurrences = [];
  
  while (i < text.length) {
    if (text[i] === pattern[j]) {
      i++;
      j++;
      
      if (j === pattern.length) {
        occurrences.push(i - j);
        j = lps[j - 1];
      }
    } else {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
  
  return occurrences;
}
```

### 3. KMP for Circular Strings

```javascript
function kmpCircular(text, pattern) {
  const doubledText = text + text;
  const lps = buildLPS(pattern);
  let i = 0, j = 0;
  
  while (i < doubledText.length && i < text.length + pattern.length - 1) {
    if (doubledText[i] === pattern[j]) {
      i++;
      j++;
      
      if (j === pattern.length) {
        return i - j;
      }
    } else {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
  
  return -1;
}
```

### 4. Case-Insensitive KMP

```javascript
function kmpCaseInsensitive(text, pattern) {
  const lowerText = text.toLowerCase();
  const lowerPattern = pattern.toLowerCase();
  const lps = buildLPS(lowerPattern);
  let i = 0, j = 0;
  
  while (i < lowerText.length) {
    if (lowerText[i] === lowerPattern[j]) {
      i++;
      j++;
      
      if (j === lowerPattern.length) {
        return i - j;
      }
    } else {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
  
  return -1;
}
```

### 5. KMP with Count

```javascript
function kmpCount(text, pattern) {
  const lps = buildLPS(pattern);
  let i = 0, j = 0;
  let count = 0;
  
  while (i < text.length) {
    if (text[i] === pattern[j]) {
      i++;
      j++;
      
      if (j === pattern.length) {
        count++;
        j = lps[j - 1];
      }
    } else {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
  
  return count;
}
```

## Optimization Techniques

### 1. Early Termination

**Stop When Pattern Found:**
```javascript
// Return first match only
// Don't continue searching
// Saves time for single match
```

### 2. Memory Optimization

**Use Efficient Data Structures:**
```javascript
// Use typed arrays for LPS
// Reduce memory footprint
// Better cache performance
```

### 3. Parallel Processing

**Search Multiple Patterns:**
```javascript
// Process multiple patterns
// Use Aho-Corasick for multi-pattern
- More efficient for many patterns
```

### 4. Hybrid Approach

**Combine with Other Algorithms:**
```javascript
// Use KMP for preprocessing
// Use Boyer-Moore for search
// Best of both worlds
```

### 5. Trade-offs

**KMP vs Other String Matching:**

| Algorithm | Time | Preprocessing | Best For |
|-----------|------|---------------|----------|
| KMP | `O(n+m)` | `O(m)` | General purpose |
| Rabin-Karp | `O(n+m)` | `O(m)` | Multiple patterns |
| Boyer-Moore | `O(n/m)` | `O(m)` | Large alphabets |
| Naive | `O(n*m)` | `O(1)` | Small texts |

**When to Use KMP:**
- General string matching
- Need all occurrences
- Pattern is fixed
- Text is large
- No wildcards needed

## Complexity Analysis

### Time Complexity

**Build LPS: O(m)**
- m = pattern length
- Single pass through pattern
- Each character processed at most twice
- Total: O(m)

**Search: O(n)**
- n = text length
- Single pass through text
- No backtracking in text
- Total: O(n)

**Total: O(n + m)**
- Linear time complexity
- Significantly better than O(n * m)
- Optimal for string matching

### Space Complexity

**Space: O(m)**
- LPS array of size m
- No additional space
- Total: O(m)

**Explanation:**
KMP achieves O(n + m) time complexity by preprocessing the pattern in O(m) time to build the LPS array, then searching the text in O(n) time with no backtracking. The space complexity is O(m) for the LPS array. This is optimal for string matching problems and significantly better than the O(n * m) time complexity of naive string matching.

## Real-world Applications

### 1. Search Engines

**Text Indexing:**
- Pattern matching in documents
- Efficient search queries
- Index building
- Example: Google Search

### 2. Content Filtering

**Pattern Detection:**
- Spam detection
- Content moderation
- Keyword filtering
- Example: Facebook content filter

### 3. Bioinformatics

**DNA Sequence Matching:**
- Gene pattern search
- Protein sequence analysis
- Genome comparison
- Example: DNA sequencing tools

### 4. Text Editors

**Find/Replace:**
- Pattern search in documents
- Replace operations
- Highlight matches
- Example: VS Code search

### 5. Log Analysis

**Pattern Search:**
- Error pattern detection
- Log file analysis
- Anomaly detection
- Example: Splunk

### 6. Plagiarism Detection

**Pattern Matching:**
- Document similarity
- Code plagiarism
- Content matching
- Example: Turnitin

### 7. Data Validation

**Pattern Matching:**
- Format validation
- Pattern checking
- Data integrity
- Example: Form validation

### 8. Network Security

**Intrusion Detection:**
- Pattern matching in packets
- Signature detection
- Traffic analysis
- Example: Snort

## Common Mistakes

### 1. Incorrect LPS Calculation

**Mistake:**
```javascript
// Wrong LPS formula
// Incorrect skip values
// Wrong results
```

**Correct:**
```javascript
// Use correct LPS algorithm
// Verify with examples
// Test thoroughly
```

**Why It Matters:**
- LPS is core to KMP
- Wrong LPS breaks algorithm
- Must be correct

### 2. Off-by-one Errors

**Mistake:**
```javascript
// Wrong index handling
// Missing +1 or -1
// Incorrect results
```

**Correct:**
```javascript
// Careful with indices
// Test with examples
// Verify indexing
```

**Why It Matters:**
- Off-by-one errors common
- Indexing is tricky
- Critical for correctness

### 3. Not Handling Empty Pattern

**Mistake:**
```javascript
// Empty pattern causes errors
// Division by zero
// Runtime error
```

**Correct:**
```javascript
// Check for empty pattern
// Return appropriate value
// Handle gracefully
```

**Why It Matters:**
- Empty pattern is valid input
- Must handle special case
- Prevents errors

### 4. Not Finding All Matches

**Mistake:**
```javascript
// Return first match only
// Miss other occurrences
// Incomplete results
```

**Correct:**
```javascript
// Continue after finding match
// Use LPS to find next
// Find all occurrences
```

**Why It Matters:**
- All matches often needed
- Incomplete results wrong
- Must continue search

### 5. Confusing LPS with Prefix Function

**Mistake:**
```javascript
// LPS != prefix function
- Different definitions
// Wrong implementation
```

**Correct:**
```javascript
// LPS is longest proper prefix
// Must be proper (not entire string)
// Correct definition
```

**Why It Matters:**
- LPS has specific definition
- Proper prefix (not entire string)
- Must use correct definition

### 6. Not Using LPS After Match

**Mistake:**
```javascript
// Reset j to 0 after match
// Miss overlapping matches
// Incomplete results
```

**Correct:**
```javascript
// Use LPS[j-1] after match
// Find overlapping matches
// Complete results
```

**Why It Matters:**
- Overlapping matches valid
- Must find all occurrences
- LPS enables this

## Advanced Concepts

### 1. Aho-Corasick Algorithm

**Concept:**
Multi-pattern string matching.

**Features:**
- Build automaton for all patterns
- Search all patterns in single pass
- O(n + m) for all patterns

### 2. Rabin-Karp Algorithm

**Concept:**
Hash-based string matching.

**Features:**
- Uses rolling hash
- Good for multiple patterns
- O(n + m) average case

### 3. Boyer-Moore Algorithm

**Concept:**
Skip characters from right to left.

**Features:**
- Bad character heuristic
- Good suffix heuristic
- O(n/m) best case

### 4. Suffix Array

**Concept:**
Array of suffixes sorted lexicographically.

**Features:**
- Advanced string operations
- Pattern matching
- O(n log n) construction

## Practice Thinking Guide

### How to Identify When to Use KMP

**Key Signals in Problem Statements:**

1. **"Find pattern in text"**
   - KMP
   - Example: "Find first occurrence"

2. **"String matching"**
   - KMP
   - Example: "Pattern matching"

3. **"Repeated substring"**
   - KMP with LPS
   - Example: "Check if repeated"

4. **"Shortest palindrome"**
   - KMP variant
   - Example: "Add characters to make palindrome"

5. **"All occurrences"**
   - KMP
   - Example: "Find all positions"

6. **"Large text"**
   - KMP
   - Example: "Search in large document"

**Pattern Recognition:**

**Pattern 1: Pattern Search**
```
Problem: Find pattern in text
Solution: KMP for efficient search
```

**Pattern 2: Repeated Substring**
```
Problem: Check if string is repeated pattern
Solution: Use LPS property
```

**Pattern 3: Shortest Palindrome**
```
Problem: Make string palindrome by adding characters
Solution: KMP with reversed string
```

**Pattern 4: Count Occurrences**
```
Problem: Count pattern occurrences
Solution: KMP with counting
```

**Pattern 5: Multiple Patterns**
```
Problem: Search multiple patterns
Solution: Aho-Corasick (not KMP)
```

**Decision Flowchart:**

```
String matching problem?
├─ Yes → Single pattern?
│        ├─ Yes → Need all occurrences?
│        │        ├─ Yes → Use KMP
│        │        └─ No → Use KMP or simpler
│        └─ No → Use Aho-Corasick
├─ No → Repeated substring check?
│        ├─ Yes → Use KMP LPS property
│        └─ No → Consider other
└─ No → Not KMP problem
```

**Example Problem Analysis:**

**Problem:** "Implement strStr()"

**Analysis:**
1. Need to find first occurrence of needle in haystack
2. Standard string search problem
3. KMP provides efficient solution
4. Return index or -1
5. Solution: KMP search

**Problem:** "Repeated substring pattern"

**Analysis:**
1. Check if string can be constructed by repeating substring
2. Use LPS property
3. If LPS[n-1] > 0 and n % (n - LPS[n-1]) == 0
4. Then repeated pattern exists
5. Solution: KMP LPS check

**Problem:** "Shortest palindrome"

**Analysis:**
1. Add characters to front to make palindrome
2. Create string + "#" + reverse(string)
3. Build LPS for combined string
4. LPS[n-1] gives longest prefix-suffix match
5. Solution: KMP with reversed string

## Summary

Knuth-Morris-Pratt (KMP) algorithm is a string matching algorithm that finds all occurrences of a pattern string within a text string in linear time O(n + m). It achieves this by preprocessing the pattern to create a Longest Prefix Suffix (LPS) array, which allows the algorithm to skip unnecessary comparisons when a mismatch occurs. KMP is fundamental to text search, pattern matching, and is used in search engines, content filtering, and bioinformatics. The key insight is that when a mismatch occurs, we don't need to start over from the beginning - we can use the LPS array to determine how many characters we can skip.

**Key Takeaways:**
- O(n + m) time complexity
- LPS array for preprocessing
- No backtracking in text
- Finds all occurrences
- Efficient for large texts
- Foundation for string algorithms
- Used in search engines
- Pattern matching essential

**Mastery Checklist:**
- ✅ Understand LPS array concept
- ✅ Implement LPS building
- ✅ Implement KMP search
- ✅ Handle edge cases
- ✅ Find all occurrences
- ✅ Understand time/space complexity
- ✅ Know when to use
- ✅ Compare with other algorithms
