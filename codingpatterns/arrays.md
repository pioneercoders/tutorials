### 📚 Array Techniques for Coding Interviews

Mastering arrays is essential for software engineers preparing for technical interviews at top tech companies like Google, Amazon, Meta, etc. This guide provides structured techniques, examples, and memory aids to solidify array concepts and boost problem-solving confidence. Arrays are one of the most fundamental and commonly tested topics in coding interviews. Mastering array patterns improves your ability to solve a wide range of problems efficiently.

#### 📌 Why Arrays Are Important?

- Arrays are used in almost all system-level and application-level programming.
- Arrays are foundational to data structures.
- Practicing arrays improves your grip on pointers, indexing, loops, and memory management.
- They are heavily tested in interviews to assess logical thinking, optimization, and understanding of memory access patterns.

**🔍 Key Techniques and Patterns**

**1️⃣ Traversal**
- Loop through elements to find min, max, or perform actions.
- Example: Find max number in an array.

**2️⃣ Two Pointers**
- Use two indexes (`i`, `j`) to solve problems without extra space.
- Common Use Cases: Sorted arrays, duplicates, reversing, partitions.
- Example: Pair sum, removing duplicates.

**3️⃣ Sliding Window**
- Efficiently handle subarray problems with fixed or dynamic window size.
- **Example:** Max sum subarray of size `k`, Longest substring without repeating characters.

**4️⃣ Prefix Sum**
- Pre-compute cumulative sums to enable fast range queries.
- Example: Subarray sum equals `k`, Range sum query.

**5️⃣ Binary Search**
- Divide and conquer for sorted arrays or monotonic functions.
- Example: Search in sorted array, find peak element.

**6️⃣ Hashing / Map-Based Lookup**
- Use hash maps/sets for fast lookups and frequency counting.
- Example: Two sum, Longest consecutive sequence.

**7️⃣ In-place Modification**
- Optimize space by modifying the array directly.
- Example: Move zeros to end, Rotate array.

**8️⃣ Sorting-Based**
- Sort first, then apply logic (especially with duplicate handling or proximity).
- Example: Merge intervals, Find the missing number.

**9️⃣ Greedy Algorithms**
- Make the best local choice at each step.
- Example: Jump Game, Distribute candies.

**🔟 Matrix Traversals**
- Navigate through 2D arrays (top/bottom/left/right or diagonals).
- **Example:** Spiral matrix, Rotate image, Search in sorted 2D matrix.

**🧪 Sample Problems by Category**

| Pattern | Problems |
|--------|----------|
| Traversal | Find max, sum of elements |
| Two Pointers | Remove duplicates, Container with most water |
| Sliding Window | Max sum subarray, Longest substring with K distinct characters |
| Prefix Sum | Subarray sum equals K, Max sum after K operations |
| Binary Search | Find element, First/Last occurrence |
| Hashing | Two sum, Find duplicates, Anagram groupings |
| In-place | Move zeroes, Rotate array |
| Greedy | Jump Game, Min Arrows to Burst Balloons |
| Matrix | Spiral traversal, Diagonal traversal |

---

**🧠 Memory Retention Techniques**

**1. Chunking**
- Break down large problems into smaller, manageable chunks.
- Example: While solving a problem, first separate input parsing, logic, and output formatting.

**2. Visualization**
- Use diagrams or tables to represent the array transformation step-by-step.

**3. Spaced Repetition**
- Practice array questions repeatedly over increasing intervals (1 day → 3 days → 7 days).

**4. Teach Back Technique**
- Explain the problem and solution to someone else (or yourself aloud).
- Reinforces understanding and highlights gaps in logic.

**5. Code → Dry Run → Debug**
- After writing code, manually dry run with sample input.
- Identify edge cases and off-by-one errors.

**🎯 Interview Tips**

- Clarify edge cases: empty array, single element, negative numbers.
- Start with brute-force; then optimize.
- Always consider time and space complexity.
- Practice dry-running your code.
- Communicate your thought process clearly.
- **Clarify the problem** before coding: Ask about constraints, input size, and edge cases.
- **Think out loud**: Communicate your approach, even before typing code.
- **Start brute-force**, then optimize.
- **Test edge cases**: empty array, single element, all duplicates, sorted/reverse sorted.
- **Optimize space/time**: Mention trade-offs between auxiliary space vs in-place solutions.

  
**📎 Final Note**

Array questions can be deceptively simple or surprisingly complex. The key is to:
- **Recognize the pattern**
- **Practice frequently**
- **Optimize step-by-step**

> “The difference between a good coder and a great coder lies in the way they use patterns.”

**🧑‍💻 Sample Code Snippets**

**🔢 Array Operations: Deletion & Dynamic Expansion**

This guide explains how to handle **element deletion** in arrays and how to **add new elements** once an array reaches its maximum capacity. These operations are crucial for building dynamic, scalable data structures.

**🗑️ Deleting an Element from an Array**

**✅ Problem Statement**
Given a fixed-size array, delete the element at a specified index and maintain the remaining element order.

**🧠 Design Approach**
- 1 Shift all elements one position to the left after the deletion index.
- 2 Optionally set the last position to a default value (`0`, `null`, etc.).

**1️⃣ Delete Element from Array (Using New Array)**

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


**2️⃣ ➕ Add Element to Array (By Copying and Creating New Array)**

**🧱 Problem**
In Java, arrays are fixed in size. To "add" an element to an array:

**🧠 Logic**
1. You create a **new array** of size `original.length + 1`.
2. **Copy** all elements from the original array.
3. Add the new element at the end.
  
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

**3️⃣ Matrix Edge Traversal and Cross (Diagonal) Traversal**
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

**🔹 Cross (Diagonal) Traversal: Primary and Secondary Diagonals**

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
