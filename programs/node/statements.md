// 1. Simple Interest Calculation
let principal = 1000;
let time = 12; // in months
let rate = 10;
let interest = (principal * time * rate) / 100;
console.log("Simple Interest:", interest);

// 2. Average of Three Numbers
let num1 = 9;
let num2 = 10;
let num3 = 8;
let average = (num1 + num2 + num3) / 3;
console.log("Average:", average);

// 3. Maximum Between Two Numbers
let a = 20;
let b = 5;
let max = a > b ? a : b;
console.log("Maximum number:", max);

// 4. Area of a Circle
let radius = 4;
let pi = 3.14;
let area = pi * radius * radius;
console.log("Area of Circle:", area);

// 5. Check Voting Eligibility
let age = 17;
if (age >= 18) {
  console.log("You are eligible to vote.");
} else {
  console.log("You are not eligible to vote.");
}

// 6. Check if Number is Positive or Negative
let number = -5;
if (number > 0) {
  console.log("The number is positive.");
} else if (number < 0) {
  console.log("The number is negative.");
} else {
  console.log("The number is zero.");
}

// 7. Grade Checker
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

// Additional Beginner-Friendly Programs:

// 8. Check Even or Odd
let num = 7;
if (num % 2 === 0) {
  console.log(num + " is even.");
} else {
  console.log(num + " is odd.");
}

// 9. Swap Two Numbers (Using a Temp Variable)
let x = 5;
let y = 10;
let temp = x;
x = y;
y = temp;
console.log("After swap: x =", x, ", y =", y);

// 10. Multiplication Table of a Number
let tableNum = 3;
console.log("Multiplication Table for", tableNum);
for (let i = 1; i <= 10; i++) {
  console.log(`${tableNum} x ${i} = ${tableNum * i}`);
}

// 11. Sum of First N Natural Numbers
let n = 5;
let sum = 0;
for (let i = 1; i <= n; i++) {
  sum += i;
}
console.log("Sum of first", n, "natural numbers:", sum);

// 12. Check Leap Year
let year = 2024;
if ((year % 4 === 0 && year % 100 !== 0) || (year % 400 === 0)) {
  console.log(year + " is a leap year.");
} else {
  console.log(year + " is not a leap year.");
}
