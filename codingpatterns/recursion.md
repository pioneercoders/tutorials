#### 🔁 Recursion Techniques for Interview Preparation (with Java Examples)

Recursion is a fundamental concept in computer science and a common topic in coding interviews. This guide walks you through recursion step-by-step with design techniques and Java examples.

**📘 What is Recursion?**

> A recursive function is a function that calls itself with smaller inputs until a base condition is met.

**🧱 Recursive Thinking: Step-by-Step Approach**

**Step 1: Identify if the problem is recursive**
- Can it be divided into smaller subproblems of the same type?

**Step 2: Define the base case**
- The simplest possible case that can be solved directly.

**Step 3: Define the recursive case**
- How to reduce the problem to a smaller version of itself.

**Step 4: Combine the result from subproblems**
- Merge results as the recursion unwinds.

## 📐 General Recursive Template

```java
public ReturnType function(InputType input) {
    if (base case condition) {
        return base result;
    }

    // smaller problem
    ReturnType smallerResult = function(smaller input);

    // combine results
    return combine(smallerResult);
}
```

✅ Problem 1: Factorial  
🧩 Problem
Find the factorial of a number n.
n! = n * (n-1) * (n-2) * ... * 1

🔄 Algorithm Steps
If n == 0, return 1 (base case).

Otherwise, return n * factorial(n - 1).

💻 Java Code

```java
public class Factorial {
    public static int factorial(int n) {
        if (n == 0) return 1; // base case
        return n * factorial(n - 1); // recursive call
    }

    public static void main(String[] args) {
        System.out.println("5! = " + factorial(5)); // Output: 120
    }
}
```

✅ Problem 2: Fibonacci  
🧩 Problem
Return the nth Fibonacci number.

🔄 Algorithm Steps
If n == 0, return 0.

If n == 1, return 1.

Otherwise, return fib(n-1) + fib(n-2).

💻 Java Code

```java
public class Fibonacci {
    public static int fib(int n) {
        if (n <= 1) return n;
        return fib(n - 1) + fib(n - 2);
    }

    public static void main(String[] args) {
        System.out.println("Fibonacci of 6 = " + fib(6)); // Output: 8
    }
}
```

✅ Problem 3: Reverse a String  
🧩 Problem  
Reverse a string using recursion.  

🔄 Algorithm Steps  
If the string is empty or has one character, return it.  

Recursively reverse the substring from index 1 and append the first character at the end.

💻 Java Code

```java
public class ReverseString {
    public static String reverse(String s) {
        if (s.length() <= 1) return s;
        return reverse(s.substring(1)) + s.charAt(0);
    }

    public static void main(String[] args) {
        System.out.println(reverse("hello")); // Output: olleh
    }
}
```

✅ Problem 4: Print Numbers from N to 1  
🧩 Problem  
Print numbers from N down to 1 using recursion.  

🔄 Algorithm Steps
If n == 0, return (stop recursion).

Print n, then call the function with n - 1.

💻 Java Code

```java
public class PrintDescending {
    public static void printDescending(int n) {
        if (n == 0) return;
        System.out.println(n);
        printDescending(n - 1);
    }

    public static void main(String[] args) {
        printDescending(5); // Output: 5 4 3 2 1
    }
}
```

✅ Problem 5: Sum of Digits  
🧩 Problem  
Given an integer n, return the sum of its digits.  

🔄 Algorithm Steps
If n == 0, return 0.

Return (n % 10) + sumDigits(n / 10).

💻 Java Code

```java
public class SumOfDigits {
    public static int sumDigits(int n) {
        if (n == 0) return 0;
        return (n % 10) + sumDigits(n / 10);
    }

    public static void main(String[] args) {
        System.out.println("Sum of digits of 1234 = " + sumDigits(1234)); // Output: 10
    }
}
```
✅ Problem 6: Check Palindrome (String)
🧩 Problem
Check whether a string is a palindrome using recursion.

🔄 Algorithm Steps
If the string has 0 or 1 characters, it's a palindrome.

If first and last characters don’t match, return false.

Else, call recursively on the substring excluding first and last characters.

💻 Java Code

```java
public class PalindromeCheck {
    public static boolean isPalindrome(String str) {
        if (str.length() <= 1) return true;
        if (str.charAt(0) != str.charAt(str.length() - 1)) return false;
        return isPalindrome(str.substring(1, str.length() - 1));
    }

    public static void main(String[] args) {
        System.out.println(isPalindrome("racecar")); // Output: true
        System.out.println(isPalindrome("hello"));   // Output: false
    }
}
```

**🧠 Recursion Patterns**

| Pattern         | Use Case                          | Example Problem                |
|-----------------|------------------------------------|---------------------------------|
| Tail Recursion  | Work done **before** return        | GCD, print numbers              |
| Head Recursion  | Work done **after** return         | Reverse string, sum of digits   |
| Tree Recursion  | Calls itself multiple times        | Fibonacci, Subsets, Permutations|
| Backtracking    | Explore all possible paths         | N-Queens, Subset generation     |


**⚠️ Recursion Tips**

- ✅ Always define the **base case** clearly.
- 🔁 Ensure each call **progresses toward the base case**.
- 🧪 Use **dry-run with small inputs** for debugging.
- 🚫 Avoid deep recursion in **performance-critical problems**.




