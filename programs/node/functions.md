<details open>
<summary>1️⃣ Write a function to add two numbers.</summary>
<p>

```javascript
function add(x, y) {
    return x + y;
}

console.log(add(5, 8));   // 13
console.log(add(9, 10));  // 19
```

</p>
</details>

<details>
<summary>2️⃣ Write a function to check if a number is even.</summary>
<p>

```javascript
function isEven(x) {
    return x % 2 === 0;
}

console.log(isEven(5));   // false
console.log(isEven(8));   // true
```

</p>
</details>

<details>
<summary>3️⃣ Write a function to multiply each element in an array by 2 and return the new array.</summary>
<p>

```javascript
function multiplyWith2(arr) {
    for (let i = 0; i < arr.length; i++) {
        arr[i] = arr[i] * 2;
    }
    return arr;
}

const numbers = [2, 5, 9, 12];                                     
console.log(multiplyWith2(numbers)); // [4, 10, 18, 24]
```

</p>
</details>

<details>
<summary>4️⃣ Write a function to find the maximum of two numbers.</summary>
<p>

```javascript
function max(x, y) {
    return (x > y) ? x : y;
}

console.log(max(8, 5));    // 8
console.log(max(9, 10));   // 10
```

</p>
</details>

<details>
<summary>5️⃣ Write a function to print numbers from 1 to n using recursion (without using loops).</summary>
<p>

```javascript
function printNumbers(n) {
    if (n === 0) return;
    printNumbers(n - 1);
    console.log(n);
}

printNumbers(10);
```

</p>
</details>

<details>
<summary>6️⃣ Write a function to return the factorial of a number using recursion.</summary>
<p>

```javascript
function factorial(n) {
    if (n === 0 || n === 1) return 1;
    return n * factorial(n - 1);
}

console.log(factorial(5));  // 120
```

</p>
</details>

<details>
<summary>7️⃣ Write a function to reverse a string.</summary>
<p>

```javascript
function reverseString(str) {
    return str.split('').reverse().join('');
}

console.log(reverseString("hello"));  // "olleh"
```

</p>
</details>

<details>
<summary>8️⃣ Write a function to check if a string is a palindrome.</summary>
<p>

```javascript
function isPalindrome(str) {
    const reversed = str.split('').reverse().join('');
    return str === reversed;
}

console.log(isPalindrome("madam"));  // true
console.log(isPalindrome("hello"));  // false
```

</p>
</details>

<details>
<summary>9️⃣ Write a function to find the sum of all elements in an array.</summary>
<p>

```javascript
function sumArray(arr) {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}

console.log(sumArray([1, 2, 3, 4, 5]));  // 15
```

</p>
</details>

<details>
<summary>🔟 Write a function to find the largest number in an array.</summary>
<p>

```javascript
function findLargest(arr) {
    let max = arr[0];
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

console.log(findLargest([2, 8, 1, 15, 4]));  // 15
```

</p>
</details>

<details>
<summary>1️⃣1️⃣ Write a function to calculate the average of an array of numbers.</summary>
<p>

```javascript
function averageArray(arr) {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum / arr.length;
}

console.log(averageArray([2, 4, 6, 8]));  // 5
```

</p>
</details>

<details>
<summary>1️⃣2️⃣ Write a function to return true if a number is prime.</summary>
<p>

```javascript
function isPrime(n) {
    if (n < 2) return false;
    for (let i = 2; i <= Math.sqrt(n); i++) {
        if (n % i === 0) return false;
    }
    return true;
}

console.log(isPrime(7));  // true
console.log(isPrime(9));  // false
```

</p>
</details>
