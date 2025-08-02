# 📚 Array Techniques for Improving Memory Retention and Cracking Coding Interviews

Mastering arrays is essential for software engineers preparing for technical interviews at top tech companies like Google, Amazon, Meta, etc. This guide provides structured techniques, examples, and memory aids to solidify array concepts and boost problem-solving confidence.

---

## 🚀 Why Focus on Arrays?

- Arrays are foundational to data structures.
- Interviewers frequently ask array-based problems to evaluate your logic, optimization skills, and problem-solving ability.
- Practicing arrays improves your grip on pointers, indexing, loops, and memory management.

---

## 🧠 Memory Retention Techniques

### 1. **Chunking**
- Break down large problems into smaller, manageable chunks.
- Example: While solving a problem, first separate input parsing, logic, and output formatting.

### 2. **Visualization**
- Use diagrams or tables to represent the array transformation step-by-step.

### 3. **Spaced Repetition**
- Practice array questions repeatedly over increasing intervals (1 day → 3 days → 7 days).

### 4. **Teach Back Technique**
- Explain the problem and solution to someone else (or yourself aloud).
- Reinforces understanding and highlights gaps in logic.

### 5. **Code → Dry Run → Debug**
- After writing code, manually dry run with sample input.
- Identify edge cases and off-by-one errors.

---

## 🔥 Must-Know Array Techniques for Interviews

| Technique | Description | Sample Problems |
|----------|-------------|------------------|
| **Two Pointer** | Use two indices to scan elements from different ends | Merge Sorted Arrays, Container with Most Water |
| **Sliding Window** | Fixed or dynamic-size window for subarrays | Maximum Sum Subarray, Longest Substring Without Repeating Characters |
| **Prefix Sum** | Pre-compute cumulative sums to answer range queries | Subarray Sum Equals K, Range Sum Query |
| **Hashing** | Use hash maps for constant-time lookups | Two Sum, Longest Consecutive Sequence |
| **Binary Search** | Apply divide-and-conquer to sorted arrays | Search in Rotated Sorted Array, Median of Two Sorted Arrays |
| **In-place Manipulation** | Modify array without extra space | Rotate Array, Move Zeroes |
| **Frequency Counting** | Track element occurrences | Majority Element, First Missing Positive |
| **Backtracking on Arrays** | Use recursion to explore all combinations | Subsets, Permutations |
| **Matrix Traversal** | Navigate 2D arrays | Spiral Order, Island Counting |
| **Greedy with Arrays** | Make optimal choices locally | Jump Game, Candy Distribution |

---

## 🧪 Practice Matrix

| Difficulty | Array Problem Type | Recommended Questions |
|------------|---------------------|------------------------|
| Easy       | Traversal, Sum, Min/Max | [Two Sum](https://leetcode.com/problems/two-sum), [Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones) |
| Medium     | Sliding Window, Prefix | [Longest Substring](https://leetcode.com/problems/longest-substring-without-repeating-characters), [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k) |
| Hard       | Greedy, DP + Array | [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water), [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray) |

---

## 🎯 Interview Tips

- **Clarify the problem** before coding: Ask about constraints, input size, and edge cases.
- **Think out loud**: Communicate your approach, even before typing code.
- **Start brute-force**, then optimize.
- **Test edge cases**: empty array, single element, all duplicates, sorted/reverse sorted.
- **Optimize space/time**: Mention trade-offs between auxiliary space vs in-place solutions.

---

## 🧑‍💻 Sample Code Snippets

### Two Sum (Hash Map Approach)
```js
function twoSum(nums, target) {
  const map = {};
  for (let i = 0; i < nums.length; i++) {
    const diff = target - nums[i];
    if (diff in map) return [map[diff], i];
    map[nums[i]] = i;
  }
}
```

# 🔢 Array Operations: Deletion & Dynamic Expansion

This guide explains how to handle **element deletion** in arrays and how to **add new elements** once an array reaches its maximum capacity. These operations are crucial for building dynamic, scalable data structures.

---

## 🗑️ Deleting an Element from an Array

### ✅ Problem Statement
Given a fixed-size array, delete the element at a specified index and maintain the remaining element order.

### 🧠 Design Approach
- Shift all elements one position to the left after the deletion index.
- Optionally set the last position to a default value (`0`, `null`, etc.).

# 🔢 Java Programs for Array Manipulation and Matrix Traversal

This document includes Java examples for:

1. Deleting an element from an array by copying to a new array
2. Adding elements to an array by creating a new array
3. Matrix edge traversal and cross (diagonal) traversal

---

## 1️⃣ Delete Element from Array (Using New Array)

```java
public class DeleteElement {
    public static int[] deleteElement(int[] arr, int indexToDelete) {
        if (indexToDelete < 0 || indexToDelete >= arr.length) {
            throw new IllegalArgumentException("Invalid index");
        }

        int[] newArray = new int[arr.length - 1];
        for (int i = 0, j = 0; i < arr.length; i++) {
            if (i != indexToDelete) {
                newArray[j++] = arr[i];
            }
        }

        return newArray;
    }

    public static void main(String[] args) {
        int[] original = {10, 20, 30, 40, 50};
        int index = 2;

        int[] result = deleteElement(original, index);

        System.out.print("After deletion: ");
        for (int num : result) {
            System.out.print(num + " ");
        }
    }
}
```


2️⃣ Add Element to Array (By Copying and Creating New Array)
```java
public class AddElement {
    public static int[] addElement(int[] arr, int newElement) {
        int[] newArray = new int[arr.length + 1];

        for (int i = 0; i < arr.length; i++) {
            newArray[i] = arr[i];
        }

        newArray[arr.length] = newElement;

        return newArray;
    }

    public static void main(String[] args) {
        int[] original = {1, 2, 3, 4};
        int newValue = 5;

        int[] result = addElement(original, newValue);

        System.out.print("After addition: ");
        for (int num : result) {
            System.out.print(num + " ");
        }
    }
}
```

3️⃣ Matrix Edge Traversal and Cross (Diagonal) Traversal
🔹 Edge Traversal (Top Row → Right Col → Bottom Row → Left Col)

```java
public class MatrixEdgeTraversal {
    public static void edgeTraversal(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;

        System.out.println("Edge Traversal:");

        // Top row
        for (int j = 0; j < cols; j++) {
            System.out.print(matrix[0][j] + " ");
        }

        // Right column
        for (int i = 1; i < rows - 1; i++) {
            System.out.print(matrix[i][cols - 1] + " ");
        }

        // Bottom row
        for (int j = cols - 1; j >= 0; j--) {
            System.out.print(matrix[rows - 1][j] + " ");
        }

        // Left column
        for (int i = rows - 2; i > 0; i--) {
            System.out.print(matrix[i][0] + " ");
        }
    }

    public static void main(String[] args) {
        int[][] matrix = {
            { 1,  2,  3,  4},
            { 5,  6,  7,  8},
            { 9, 10, 11, 12},
            {13, 14, 15, 16}
        };

        edgeTraversal(matrix);
    }
}
```

🔹 Cross (Diagonal) Traversal: Primary and Secondary Diagonals

```java
public class MatrixDiagonalTraversal {
    public static void crossDiagonalTraversal(int[][] matrix) {
        int n = matrix.length;

        System.out.print("Primary Diagonal: ");
        for (int i = 0; i < n; i++) {
            System.out.print(matrix[i][i] + " ");
        }

        System.out.print("\nSecondary Diagonal: ");
        for (int i = 0; i < n; i++) {
            System.out.print(matrix[i][n - 1 - i] + " ");
        }
    }

    public static void main(String[] args) {
        int[][] matrix = {
            { 1,  2,  3},
            { 4,  5,  6},
            { 7,  8,  9}
        };

        crossDiagonalTraversal(matrix);
    }
}
```
