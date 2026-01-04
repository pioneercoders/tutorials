# String Basics & Techniques for Interview Preparation (Java)

Strings are one of the **most commonly asked topics** in coding interviews. Almost every interview—especially for **Java roles**—starts with string-based problems to test fundamentals, logic, and problem-solving skills.

This blog covers **string basics + essential techniques**, with **Java examples**, **interview insights**, and **common questions**.

---

## 1. What is a String in Java?

A **String** is a sequence of characters.

```java
String str = "Interview";
```

### Key Points

* `String` is a **class**, not a primitive type
* Strings in Java are **immutable**
* Stored in **String Constant Pool** (for literals)

### Interview Question

**Q:** Is String mutable or immutable in Java?

---

## 2. String Immutability (Very Important)

Once created, a String object **cannot be changed**.

```java
String s = "java";
s.concat(" interview");
System.out.println(s); // java
```

A new object is created, but `s` still points to the old one.

### Why Immutability?

* Security
* Thread safety
* Performance optimization (String Pool)

---

## 3. String Constant Pool (SCP)

```java
String a = "amazon";
String b = "amazon";
System.out.println(a == b); // true
```

Both references point to the **same object** in SCP.

```java
String c = new String("amazon");
System.out.println(a == c); // false
```

### Interview Question

**Q:** Difference between `==` and `.equals()`?

---

## 4. Common String Methods (Must Know)

| Method          | Description                       |
| --------------- | --------------------------------- |
| `length()`      | Returns length                    |
| `charAt()`      | Character at index                |
| `substring()`   | Extracts part of string           |
| `toLowerCase()` | Converts to lowercase             |
| `toUpperCase()` | Converts to uppercase             |
| `trim()`        | Removes leading & trailing spaces |
| `split()`       | Splits string                     |

```java
String s = "Coding";
System.out.println(s.charAt(0)); // C
System.out.println(s.substring(1, 4)); // odi
```

---

## 5. Traversing a String

### Using for-loop

```java
for (int i = 0; i < s.length(); i++) {
    System.out.print(s.charAt(i));
}
```

### Using for-each loop

```java
for (char ch : s.toCharArray()) {
    System.out.print(ch);
}
```

### Interview Question

**Q:** Why can’t we directly use for-each on String?

---

## 6. Character Comparison & ASCII Values

Characters are internally stored as **ASCII values**.

```java
char c = 'A';
if (c >= 'A' && c <= 'Z') {
    System.out.println("Uppercase letter");
}
```

This logic is commonly used in:

* Case conversion
* Validation problems

---

## 7. StringBuilder vs StringBuffer vs String

| Feature     | String | StringBuilder | StringBuffer |
| ----------- | ------ | ------------- | ------------ |
| Mutable     | ❌      | ✅             | ✅            |
| Thread-safe | ✅      | ❌             | ✅            |
| Performance | Slow   | Fast          | Medium       |

```java
StringBuilder sb = new StringBuilder("hello");
sb.append(" world");
```

### Interview Question

**Q:** Why is StringBuilder faster than String?

---

## 8. Reversing a String (Basic Technique)

### Efficient Way

```java
String s = "amazon";
String reversed = new StringBuilder(s).reverse().toString();
```

### Manual Way

```java
String result = "";
for (int i = s.length() - 1; i >= 0; i--) {
    result += s.charAt(i);
}
```

⚠️ Manual way is inefficient due to immutability.

---

## 9. Palindrome Check (Two Pointers Technique)

```java
String s = "madam";
int left = 0, right = s.length() - 1;

while (left < right) {
    if (s.charAt(left) != s.charAt(right)) {
        System.out.println("Not Palindrome");
        return;
    }
    left++;
    right--;
}
System.out.println("Palindrome");
```

---

## 10. Frequency Counting in String

```java
String s = "banana";
int[] freq = new int[26];

for (char c : s.toCharArray()) {
    freq[c - 'a']++;
}
```

Used in:

* Anagram problems
* First unique character

---



