<details open>
<summary>1️⃣ Write a program to check whether a number is odd or even.</summary>
<p>

```javascript
function checkOddEven(number) {
    if (number % 2 === 0) {
        console.log(`${number} is Even`);
    } else {
        console.log(`${number} is Odd`);
    }
}

checkOddEven(10);
checkOddEven(7);
```

</p>
</details>

<details>
<summary>2️⃣ Write a program to find the largest among three numbers.</summary>
<p>

```javascript
function findLargest(a, b, c) {
    if (a >= b && a >= c) {
        console.log(`${a} is the largest`);
    } else if (b >= a && b >= c) {
        console.log(`${b} is the largest`);
    } else {
        console.log(`${c} is the largest`);
    }
}

findLargest(10, 5, 8);
```

</p>
</details>

<details>
<summary>3️⃣ Write a program to calculate the sum of digits of a number.</summary>
<p>

```javascript
function sumOfDigits(num) {
    let sum = 0;
    while (num != 0) {
        sum += num % 10;
        num = Math.floor(num / 10);
    }
    console.log("Sum of digits:", sum);
}

sumOfDigits(1234);
```

</p>
</details>

<details>
<summary>4️⃣ Write a program to reverse a number.</summary>
<p>

```javascript
function reverseNumber(num) {
    let reverse = 0;
    while (num !== 0) {
        reverse = reverse * 10 + (num % 10);
        num = Math.floor(num / 10);
    }
    console.log("Reversed Number:", reverse);
}

reverseNumber(1234);
```

</p>
</details>

<details>
<summary>5️⃣ Write a program to generate multiplication table of a number.</summary>
<p>

```javascript
function multiplicationTable(num) {
    for (let i = 1; i <= 10; i++) {
        console.log(`${num} x ${i} = ${num * i}`);
    }
}

multiplicationTable(7);
```

</p>
</details>

<details>
<summary>6️⃣ Write a program to count vowels in a given string.</summary>
<p>

```javascript
function countVowels(str) {
    const vowels = ['a', 'e', 'i', 'o', 'u'];
    let count = 0;
    for (const char of str.toLowerCase()) {
        if (vowels.includes(char)) {
            count++;
        }
    }
    console.log(`Number of vowels: ${count}`);
}

countVowels("JavaScript Programming");
```

</p>
</details>

<details>
<summary>7️⃣ Write a program to print Fibonacci series up to n terms.</summary>
<p>

```javascript
function printFibonacci(n) {
    let n1 = 0, n2 = 1, nextTerm;

    console.log(n1);
    console.log(n2);

    for (let i = 3; i <= n; i++) {
        nextTerm = n1 + n2;
        console.log(nextTerm);
        n1 = n2;
        n2 = nextTerm;
    }
}

printFibonacci(8);
```

</p>
</details>

<details>
<summary>8️⃣ Write a program to find the GCD (Greatest Common Divisor) of two numbers.</summary>
<p>

```javascript
function findGCD(a, b) {
    while (b != 0) {
        let temp = b;
        b = a % b;
        a = temp;
    }
    console.log("GCD is:", a);
}

findGCD(24, 36);
```

</p>
</details>

<details>
<summary>9️⃣ Write a program to check whether a number is prime.</summary>
<p>

```javascript
function isPrime(num) {
    if (num <= 1) return false;

    for (let i = 2; i <= Math.sqrt(num); i++) {
        if (num % i === 0) return false;
    }
    return true;
}

let number = 13;
console.log(`${number} is prime?`, isPrime(number));
```

</p>
</details>

<details>
<summary>🔟 Write a program to calculate the power of a number using a loop.</summary>
<p>

```javascript
function power(base, exponent) {
    let result = 1;
    for (let i = 0; i < exponent; i++) {
        result *= base;
    }
    console.log(`${base} raised to ${exponent} is ${result}`);
}

power(2, 4);
```

</p>
</details>

<details>
<summary>1️⃣1️⃣ Write a program to find if a given number is an Armstrong number or not.</summary>
<p>

```javascript
// program to check an Armstrong number of three digits
let sum = 0;
const number = prompt('Enter a three-digit positive integer: ');

// create a temporary variable
let temp = number;
while (temp > 0) {
    // finding the one's digit
    let remainder = temp % 10;
    sum += remainder * remainder * remainder;
    // removing last digit from the number
    temp = parseInt(temp / 10);
}

// check the condition
if (sum == number) {
    console.log(`${number} is an Armstrong number`);
} else {
    console.log(`${number} is not an Armstrong number.`);
}
```

</p>
</details>

<details>
<summary>1️⃣2️⃣ Write a program to find the factorial of a given number.</summary>
<p>

```javascript
function factorial(n) {
    let answer = 1;
    if (n == 0 || n == 1) {
        return answer;
    } else if (n > 1) {
        for (let i = n; i >= 1; i--) {
            answer = answer * i;
        }
        return answer;
    } else {
        return "Number has to be positive.";
    }
}

const n = 4;
const answer = factorial(n);
console.log("Factorial of " + n + " : " + answer);
```

</p>
</details>

<details>
<summary>1️⃣3️⃣ Write a program to check if a string is a palindrome or not.</summary>
<p>

```javascript
// program to check if the string is palindrome or not

function checkPalindrome(string) {
    // find the length of a string
    const len = string.length;

    // loop through half of the string
    for (let i = 0; i < len / 2; i++) {
        // check if first and last string are same
        if (string[i] !== string[len - 1 - i]) {
            return 'It is not a palindrome';
        }
    }
    return 'It is a palindrome';
}

// take input
const string = prompt('Enter a string: ');

// call the function
const value = checkPalindrome(string);

console.log(value);
```

</p>
</details>

<details>
<summary>1️⃣4️⃣ Write a program to print a right-aligned star pattern.</summary>
<p>

```javascript
const n = 5;
let string = "";

for (let i = 1; i <= n; i++) {
    // printing spaces
    for (let j = 0; j < n - i; j++) {
        string += " ";
    }
    // printing stars
    for (let k = 0; k < i; k++) {
        string += "*";
    }
    string += "\n";
}
console.log(string);
```

</p>
</details>
