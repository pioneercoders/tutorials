# 🧠 Backtracking Techniques for Solving Coding Problems

Backtracking is a powerful algorithmic technique for solving problems recursively by trying to build a solution incrementally and removing those solutions that fail to satisfy the constraints.

---

## ✅ When to Use Backtracking

Use backtracking when:
- The problem asks for **all** solutions or **any one valid** solution.
- You are exploring **combinations**, **permutations**, **subsets**, or **partitions**.
- The solution space is **huge**, and you need **pruning** (skip bad candidates early).

---

## 🛠 General Backtracking Template

```java
void backtrack(State state) {
    if (goalReached(state)) {
        // process result
        return;
    }

    for (choice : availableChoices(state)) {
        if (isValid(choice, state)) {
            makeChoice(choice, state);         // choose
            backtrack(state);                  // explore
            undoChoice(choice, state);         // un-choose (backtrack)
        }
    }
}
```

🧩 Example 1: Subsets of an Array
Problem: Given an integer array, return all possible subsets (the power set).

🧮 Algorithmic Steps
1. Start with an empty list current to build subsets.
2. At each step, add current to the final result.
3. Loop through remaining elements from the current index:
4. Add the element to current (choose).
5. Recursively call backtrack from the next index (explore).
6. Remove the element from current (un-choose).
7. Repeat this process until all subsets are generated.

```java
import java.util.*;

public class SubsetsBacktracking {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(0, nums, new ArrayList<>(), result);
        return result;
    }

    void backtrack(int start, int[] nums, List<Integer> current, List<List<Integer>> result) {
        result.add(new ArrayList<>(current));
        for (int i = start; i < nums.length; i++) {
            current.add(nums[i]);                      // choose
            backtrack(i + 1, nums, current, result);   // explore
            current.remove(current.size() - 1);        // un-choose
        }
    }

    public static void main(String[] args) {
        SubsetsBacktracking sb = new SubsetsBacktracking();
        System.out.println(sb.subsets(new int[]{1, 2, 3}));
    }
}
```

🧩 Example 2: Permutations
Problem: Given a list of distinct integers, return all possible permutations.

🧮 Algorithmic Steps
1. Use a list current to build a permutation and a boolean array used[] to track used elements.
2. If current length equals input length, add to result (base case).
3. Loop through each element:
4. If it's already used, skip.
5. Mark it as used and add it to current (choose).
6. Recursively call backtrack (explore).
7. Remove it from current and mark as unused (un-choose).
8. Repeat this process to generate all permutations.

```
import java.util.*;

public class PermutationsBacktracking {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        boolean[] used = new boolean[nums.length];
        backtrack(nums, new ArrayList<>(), used, result);
        return result;
    }

    void backtrack(int[] nums, List<Integer> current, boolean[] used, List<List<Integer>> result) {
        if (current.size() == nums.length) {
            result.add(new ArrayList<>(current));
            return;
        }

        for (int i = 0; i < nums.length; i++) {
            if (used[i]) continue; // skip used
            used[i] = true;                         // choose
            current.add(nums[i]);
            backtrack(nums, current, used, result); // explore
            current.remove(current.size() - 1);     // un-choose
            used[i] = false;
        }
    }

    public static void main(String[] args) {
        PermutationsBacktracking pb = new PermutationsBacktracking();
        System.out.println(pb.permute(new int[]{1, 2, 3}));
    }
}
```

#### 🧠 Algorithmic Steps (Backtracking Pattern)
Define the state:

**What do you need to track? (e.g., path, index, used flags)**

**Decide when to stop:**
Base case for recursive termination (goal reached).
**Loop through choices:**
Try all possibilities from current state.
**Check constraints (optional):**
Prune the tree early if the current path violates a constraint.
**Make a choice:**
Modify the current state.
**Recurse:**
Move forward to explore further.
**Undo the choice:**
Backtrack to previous state.


