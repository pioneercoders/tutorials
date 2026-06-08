# Strings in Data Structures & Algorithms

Strings are one of the most important topics in software engineering.

Almost every modern application heavily depends on strings:

* Search engines
* Chat applications
* Compilers
* AI systems
* DNA sequencing
* Autocomplete systems
* Password validation
* Text editors
* Web browsers

In coding interviews, string problems are extremely common because they test:

* Logic
* Pattern recognition
* Optimization skills
* Algorithmic thinking

---

# 1. String Basics

A **String** is a sequence of characters.

```js id="2c19hy"
const name = "Gowtham";
```

Characters include:

* Letters
* Numbers
* Symbols
* Emojis
* Unicode characters

---

# Internal Representation

Strings are internally stored as arrays of characters.

```text id="mx78lg"
"GOWTHAM"

Index:
0 1 2 3 4 5 6

G O W T H A M
```

---

# String Indexing

```js id="h29vhh"
const str = "hello";

console.log(str[0]); // h
console.log(str[4]); // o
```

---

# Time Complexity

| Operation        | Complexity |
| ---------------- | ---------- |
| Access Character | O(1)       |
| Traverse String  | O(n)       |
| Concatenation    | O(n)       |
| Search           | O(n)       |

---

# Real-Time Applications

| Application   | Usage               |
| ------------- | ------------------- |
| WhatsApp      | Messages            |
| Google Search | Query matching      |
| VS Code       | Code parsing        |
| Browsers      | HTML/CSS processing |
| AI Chatbots   | NLP processing      |

---

# 2. Immutable vs Mutable Strings

This is a very important interview topic.

---

# Immutable Strings

Cannot be modified after creation.

JavaScript strings are immutable.

---

# Example

```js id="pzmjlwm"
let str = "hello";

str[0] = "H";

console.log(str);
```

Output:

```text id="t7h6dq"
hello
```

Nothing changes.

---

# Why Immutable?

Advantages:

* Security
* Thread safety
* Easier caching
* Predictable behavior

---

# Real-Time Example

## Browser URLs

Immutable URLs prevent accidental modification.

---

# Mutable Strings

Can be changed directly.

Languages like:

* C++
* Java (StringBuilder)
* Python lists workaround

support mutable approaches.

---

# Example Using Array

```js id="s8ur3m"
let chars = ["h", "e", "l", "l", "o"];

chars[0] = "H";

console.log(chars.join(""));
```

---

# Why Mutable Structures Matter

Efficient for:

* Heavy editing
* Large text processing
* Compilers
* Text editors

---

# Immutable vs Mutable Comparison

| Feature      | Immutable          | Mutable          |
| ------------ | ------------------ | ---------------- |
| Modification | Creates new object | Changes existing |
| Memory       | More allocations   | Efficient        |
| Safety       | High               | Lower            |
| Performance  | Slower edits       | Faster edits     |

---

# 3. String Operations

---

# Concatenation

```js id="3qjxgd"
const first = "Hello";
const second = "World";

const result = first + " " + second;

console.log(result);
```

---

# Length

```js id="m49mpm"
console.log(result.length);
```

---

# Substring

```js id="2gyn2x"
const str = "JavaScript";

console.log(str.substring(0, 4));
```

Output:

```text id="d9w56k"
Java
```

---

# Split

```js id="jlwmvf"
const sentence = "I love coding";

console.log(sentence.split(" "));
```

---

# Reverse String

```js id="qfhskx"
function reverse(str) {
  return str.split("").reverse().join("");
}
```

---

# Palindrome Check

```js id="d4eqk2"
function isPalindrome(str) {
  return str === str.split("").reverse().join("");
}
```

---

# Frequency Count

```js id="78zfdx"
function frequency(str) {
  const map = {};

  for (const char of str) {
    map[char] = (map[char] || 0) + 1;
  }

  return map;
}
```

---

# Real-Time Example

## Password Validation

Checks:

* Length
* Symbols
* Patterns
* Character frequency

---

# 4. Character Encoding

Computers store everything as numbers.

Characters are converted into numeric values using encoding systems.

---

# ASCII

American Standard Code for Information Interchange.

Uses:

* 7 bits
* 128 characters

---

# Example

| Character | ASCII |
| --------- | ----- |
| A         | 65    |
| a         | 97    |
| 0         | 48    |

---

# JavaScript Example

```js id="y0vzvl"
console.log("A".charCodeAt(0));
```

---

# Unicode

ASCII was limited.

Unicode supports:

* All languages
* Emojis
* Symbols

---

# Example

| Character | Unicode |
| --------- | ------- |
| A         | U+0041  |
| ₹         | U+20B9  |
| 😀        | U+1F600 |

---

# UTF-8

UTF-8 is the most widely used encoding.

Features:

* Variable length
* Memory efficient
* Backward compatible with ASCII

---

# Why UTF-8 Matters

Used everywhere:

* Web browsers
* APIs
* Databases
* JSON
* HTTP

---

# Real-Time Example

Without Unicode:

* Hindi
* Telugu
* Chinese
* Emojis

would break on websites.

---

# 5. Pattern Matching

Finding patterns inside text.

Core problem in:

* Search engines
* Antivirus software
* DNA analysis
* NLP systems

---

# Naive Pattern Matching

```js id="5k50j5"
function search(text, pattern) {
  for (let i = 0; i <= text.length - pattern.length; i++) {
    let j = 0;

    while (
      j < pattern.length &&
      text[i + j] === pattern[j]
    ) {
      j++;
    }

    if (j === pattern.length) {
      return i;
    }
  }

  return -1;
}
```

---

# Complexity

| Case  | Complexity |
| ----- | ---------- |
| Worst | O(n × m)   |

Where:

* n = text length
* m = pattern length

---

# Real-Time Example

## Browser Find Feature

Ctrl + F uses pattern matching internally.

---

# 6. Rabin-Karp Algorithm

Uses hashing for efficient pattern matching.

Instead of comparing full strings:

* Compare hashes first.

---

# Core Idea

```text id="n7f3xh"
If hash(text window) == hash(pattern)
then compare actual characters
```

---

# Rolling Hash Concept

Efficiently update hash while sliding window.

---

# Example

```js id="0u2hzb"
function hash(str) {
  let h = 0;

  for (const char of str) {
    h += char.charCodeAt(0);
  }

  return h;
}
```

---

# Complexity

| Average | O(n + m) |
| ------- | -------- |
| Worst   | O(n × m) |

---

# Real-Time Applications

| System               | Usage                  |
| -------------------- | ---------------------- |
| Plagiarism detection | Document matching      |
| Malware scanning     | Signature matching     |
| DNA sequencing       | Pattern identification |

---

# 7. KMP Algorithm (Knuth-Morris-Pratt)

One of the most important string algorithms.

Optimizes pattern matching by avoiding unnecessary comparisons.

---

# Main Idea

When mismatch occurs:

* Use previous match information
* Do not restart from scratch

---

# LPS Array

LPS:

```text id="xz8kff"
Longest Prefix Suffix
```

Stores reusable pattern information.

---

# Example

Pattern:

```text id="qpjg4g"
ABABCABAB
```

LPS:

```text id="f8cs3h"
0 0 1 2 0 1 2 3 4
```

---

# KMP Complexity

| Complexity | Value    |
| ---------- | -------- |
| Time       | O(n + m) |
| Space      | O(m)     |

---

# Why KMP is Powerful

No backtracking in text.

Very efficient for large-scale searching.

---

# Real-Time Applications

| System         | Usage               |
| -------------- | ------------------- |
| Search engines | Fast searching      |
| IDEs           | Syntax highlighting |
| DNA analysis   | Sequence search     |

---

# Simplified KMP Implementation

```js id="hcd8c6"
function buildLPS(pattern) {
  const lps = Array(pattern.length).fill(0);

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
```

---

# 8. Z Algorithm

Another efficient pattern matching algorithm.

Builds Z-array.

---

# Z[i]

Length of substring starting at i
that matches prefix.

---

# Example

```text id="jlwmz1"
String: aabxaabxcaabxaabxay
```

---

# Complexity

| Complexity | Value |
| ---------- | ----- |
| Time       | O(n)  |

---

# Applications

* Pattern matching
* String compression
* Bioinformatics

---

# Why Z Algorithm Matters

Very useful in competitive programming.

Simpler than KMP in some scenarios.

---

# 9. Trie-Based String Search

Trie is a tree-like structure for strings.

---

# Visualization

```text id="4f7hlj"
        root
       /    \
      c      d
     /        \
    a          o
   /            \
  t              g
```

Words:

* cat
* dog

---

# Features

| Operation     | Complexity |
| ------------- | ---------- |
| Insert        | O(length)  |
| Search        | O(length)  |
| Prefix Search | O(length)  |

---

# Basic Trie Node

```js id="u7p0lf"
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}
```

---

# Real-Time Applications

| System              | Usage            |
| ------------------- | ---------------- |
| Google autocomplete | Suggestions      |
| Dictionary apps     | Word lookup      |
| Search engines      | Prefix search    |
| IDE autocomplete    | Code suggestions |

---

# Why Trie is Fast

Instead of scanning all words:

* Navigate character by character.

---

# 10. Rolling Hashing

Efficient hash recalculation technique.

Very important for:

* Rabin-Karp
* Substring comparison
* Duplicate detection

---

# Core Idea

Instead of recalculating full hash:

* Remove old character
* Add new character

---

# Example

```text id="xlct44"
Window 1: abc
Window 2: bcd
```

Reuse previous computation.

---

# Formula

```text id="4y4ctc"
newHash =
(oldHash - oldChar × power) × base + newChar
```

---

# Complexity

| Operation   | Complexity |
| ----------- | ---------- |
| Update Hash | O(1)       |

---

# Real-Time Applications

| System             | Usage                  |
| ------------------ | ---------------------- |
| Git                | File comparison        |
| Data deduplication | Duplicate detection    |
| Plagiarism systems | Content matching       |
| Blockchain         | Integrity verification |

---

# Important Interview Patterns in Strings

| Pattern        | Example Problems    |
| -------------- | ------------------- |
| Sliding Window | Longest substring   |
| Two Pointer    | Palindromes         |
| Hashing        | Duplicate substring |
| Trie           | Autocomplete        |
| KMP            | Pattern matching    |
| DP on Strings  | Edit distance       |

---

# Common String Interview Problems

1. Valid Anagram
2. Longest Palindrome
3. Group Anagrams
4. Longest Substring Without Repeating Characters
5. Minimum Window Substring
6. String Compression
7. Implement strstr()
8. Rabin-Karp Search
9. Regular Expression Matching
10. Word Break Problem

---

# Common Beginner Mistakes

| Mistake                      | Problem            |
| ---------------------------- | ------------------ |
| Ignoring immutability        | Performance issues |
| Repeated concatenation       | O(n²) behavior     |
| Wrong encoding assumptions   | Unicode bugs       |
| Forgetting edge cases        | Empty strings      |
| Using brute force everywhere | Slow solutions     |

---

# Production Engineering Insights

String processing powers:

* Search engines
* AI chatbots
* Recommendation systems
* Voice assistants
* Compilers
* Cybersecurity systems

Modern systems process:

* Billions of strings daily

Efficiency matters enormously.

---

# Summary Table

| Topic             | Key Idea                 |
| ----------------- | ------------------------ |
| String Basics     | Sequence of characters   |
| Immutable Strings | Cannot change            |
| Mutable Strings   | Editable                 |
| Encoding          | Character representation |
| Pattern Matching  | Find substrings          |
| Rabin-Karp        | Hash-based search        |
| KMP               | Efficient pattern reuse  |
| Z Algorithm       | Prefix matching          |
| Trie              | Prefix tree              |
| Rolling Hash      | Fast hash updates        |

---
