<details open>
<summary>1️⃣ Write a function to count the number of words in a string.</summary>
<p>

```javascript
function countWords(str) {
    return str.trim().split(/\s+/).length;
}

const result = countWords("Hi welcome to Coding Krishna website.");
console.log(result); // 5
```

</p>
</details>

<details>
<summary>2️⃣ Write a function to compare two strings (case-sensitive).</summary>
<p>

```javascript
function compareStr(str1, str2) {
    return str1 === str2;
}

console.log(compareStr("codingkrishna", "codingkrishna")); // true
console.log(compareStr("Hello", "hello")); // false
```

</p>
</details>

<details>
<summary>3️⃣ Write a function to reverse a string.</summary>
<p>

```javascript
function reverseString(str) {
    return str.split('').reverse().join('');
}

console.log(reverseString("coding")); // "gnidoc"
```

</p>
</details>

<details>
<summary>4️⃣ Write a function to convert a string to uppercase.</summary>
<p>

```javascript
function toUpperCaseStr(str) {
    return str.toUpperCase();
}

console.log(toUpperCaseStr("coding krishna")); // "CODING KRISHNA"
```

</p>
</details>

<details>
<summary>5️⃣ Write a function to convert a string to lowercase.</summary>
<p>

```javascript
function toLowerCaseStr(str) {
    return str.toLowerCase();
}

console.log(toLowerCaseStr("CODING KRISHNA")); // "coding krishna"
```

</p>
</details>

<details>
<summary>6️⃣ Write a function to check if a string contains another string.</summary>
<p>

```javascript
function contains(str, substr) {
    return str.includes(substr);
}

console.log(contains("Welcome to codingkrishna", "coding")); // true
console.log(contains("Welcome to codingkrishna", "python")); // false
```

</p>
</details>

<details>
<summary>7️⃣ Write a function to count the number of characters in a string (excluding spaces).</summary>
<p>

```javascript
function countCharacters(str) {
    return str.replace(/\s/g, '').length;
}

console.log(countCharacters("Coding Krishna Site")); // 17
```

</p>
</details>

<details>
<summary>8️⃣ Write a function to extract a substring from a string.</summary>
<p>

```javascript
function extractSubstring(str, start, end) {
    return str.substring(start, end);
}

console.log(extractSubstring("Coding Krishna", 0, 6)); // "Coding"
```

</p>
</details>

<details>
<summary>9️⃣ Write a function to check if a string is a palindrome.</summary>
<p>

```javascript
function isPalindrome(str) {
    const cleanStr = str.replace(/\s+/g, '').toLowerCase();
    return cleanStr === cleanStr.split('').reverse().join('');
}

console.log(isPalindrome("madam")); // true
console.log(isPalindrome("Coding Krishna")); // false
```

</p>
</details>

<details>
<summary>🔟 Write a function to repeat a string multiple times.</summary>
<p>

```javascript
function repeatString(str, count) {
    return str.repeat(count);
}

console.log(repeatString("Hi ", 3)); // "Hi Hi Hi "
```

</p>
</details>

<details>
<summary>1️⃣1️⃣ Write a function to remove spaces from a string.</summary>
<p>

```javascript
function removeSpaces(str) {
    return str.replace(/\s+/g, '');
}

console.log(removeSpaces("Coding Krishna Rocks")); // "CodingKrishnaRocks"
```

</p>
</details>

<details>
<summary>1️⃣2️⃣ Write a function to find the index of a substring in a string.</summary>
<p>

```javascript
function indexOfSubstring(str, substr) {
    return str.indexOf(substr);
}

console.log(indexOfSubstring("Welcome to codingkrishna", "coding")); // 11
console.log(indexOfSubstring("Welcome to codingkrishna", "python")); // -1
```

</p>
</details>
