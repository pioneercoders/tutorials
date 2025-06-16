<details open>
<summary>1️⃣ Write a program to find Simple Interest.</summary>

```javascript
let principal = 1000;
let time = 12;
let rate = 10;
let interest = (principal * time * rate) / 100;
console.log("Simple Interest is: " + interest);
```

</details>

<details>
<summary>2️⃣ Write a program to print average of 3 numbers.</summary>

```javascript
let num1 = 9;
let num2 = 10;
let num3 = 8;
let average = (num1 + num2 + num3) / 3;
console.log("Average is: " + average);
```

</details>

<details>
<summary>3️⃣ Write a program to get max number between 2 numbers.</summary>

```javascript
let num1 = 20;
let num2 = 5;
let maxNum = (num1 > num2) ? num1 : num2;
console.log("Maximum number is: " + maxNum);
```

</details>

<details>
<summary>4️⃣ Write a program to find the area of a circle.</summary>

```javascript
let radius = 4;
const PI = 3.14;
let area = PI * radius * radius;
console.log("Area of circle is: " + area);
```

</details>

<details>
<summary>5️⃣ Write a program to check if a person is eligible to vote.</summary>

```javascript
let age = 17;

if (age >= 18) {
    console.log("You are eligible to vote.");
} else {
    console.log("You are not eligible to vote.");
}
```

</details>

<details>
<summary>6️⃣ Write a program to check if a number is positive or negative.</summary>

```javascript
let number = -5;

if (number > 0) {
    console.log("The number is positive.");
} else if (number < 0) {
    console.log("The number is negative.");
} else {
    console.log("The number is zero.");
}
```

</details>

<details>
<summary>7️⃣ Write a program for a simple grade checker.</summary>

```javascript
let score = 75;

if (score >= 90) {
    console.log("Grade: A");
} else if (score >= 75) {
    console.log("Grade: B");
} else if (score >= 60) {
    console.log("Grade: C");
} else {
    console.log("Grade: F");
}
```

</details>

<details>
<summary>8️⃣ Write a program to check if a number is even or odd.</summary>

```javascript
let number = 7;

if (number % 2 === 0) {
    console.log(number + " is Even");
} else {
    console.log(number + " is Odd");
}
```

</details>

<details>
<summary>9️⃣ Write a program to print the largest of three numbers.</summary>

```javascript
let a = 5;
let b = 12;
let c = 9;

if (a >= b && a >= c) {
    console.log(a + " is the largest number.");
} else if (b >= a && b >= c) {
    console.log(b + " is the largest number.");
} else {
    console.log(c + " is the largest number.");
}
```

</details>

<details>
<summary>🔟 Write a program to check whether a year is a leap year or not.</summary>

```javascript
let year = 2024;

if ((year % 4 === 0 && year % 100 !== 0) || year % 400 === 0) {
    console.log(year + " is a Leap Year");
} else {
    console.log(year + " is Not a Leap Year");
}
```

</details>

<details>
<summary>1️⃣1️⃣ Write a program to assign grade based on marks using switch case.</summary>

```javascript
let marks = 85;
let grade;

switch (true) {
    case (marks >= 90):
        grade = "A";
        break;
    case (marks >= 75):
        grade = "B";
        break;
    case (marks >= 60):
        grade = "C";
        break;
    default:
        grade = "F";
}
console.log("Grade: " + grade);
```

</details>

<details>
<summary>1️⃣2️⃣ Write a program to print numbers from 1 to 5 using a for loop.</summary>

```javascript
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

</details>

<details>
<summary>1️⃣3️⃣ Write a program to print multiplication table of a number.</summary>

```javascript
let num = 3;

for (let i = 1; i <= 10; i++) {
    console.log(num + " x " + i + " = " + (num * i));
}
```

</details>

<details>
<summary>1️⃣4️⃣ Write a program to calculate factorial of a number.</summary>

```javascript
let number = 5;
let factorial = 1;

for (let i = 1; i <= number; i++) {
    factorial *= i;
}

console.log("Factorial of " + number + " is " + factorial);
```

</details>
