<details open>
<summary>1️⃣ Arithmetic Operators (Addition, Subtraction, etc.)</summary>
<p>

```javascript
let a = 10;
let b = 5;

console.log("Addition:", a + b);           // 15
console.log("Subtraction:", a - b);        // 5
console.log("Multiplication:", a * b);     // 50
console.log("Division:", a / b);           // 2
console.log("Modulo (Remainder):", a % b); // 0
```

</p>
</details>

<details>
<summary>2️⃣ Comparison Operators (==, ===, !=, >, <, etc.)</summary>
<p>

```javascript
let x = 10;
let y = "10";

console.log("== :", x == y);    // true  (loose equality)
console.log("!= :", x != y);    // false
console.log("=== :", x === y);  // false (strict equality)
console.log("!== :", x !== y);  // true

let a = 8;
let b = 5;
console.log("> :", a > b);      // true
console.log("< :", a < b);      // false
console.log(">= :", a >= b);    // true
console.log("<= :", a <= b);    // false
```

</p>
</details>

<details>
<summary>3️⃣ Logical Operators (AND, OR, NOT)</summary>
<p>

```javascript
let hasPermission = true;
let isLoggedIn = false;

console.log("AND (&&):", hasPermission && isLoggedIn); // false
console.log("OR (||):", hasPermission || isLoggedIn);  // true
console.log("NOT (!):", !hasPermission);               // false
```

</p>
</details>

<details>
<summary>4️⃣ Bitwise Operators (&, |, ^, <<, >>)</summary>
<p>

```javascript
let x = 10; // 1010
let y = 5;  // 0101

console.log("AND (&):", x & y);     // 0
console.log("OR (|):", x | y);      // 15
console.log("XOR (^):", x ^ y);     // 15
console.log("Left Shift (<<):", x << 1); // 20
console.log("Right Shift (>>):", x >> 1); // 5
```

</p>
</details>

<details>
<summary>5️⃣ Assignment Operators (=, +=, -=, etc.)</summary>
<p>

```javascript
let x = 10;

x += 5;  // x = x + 5
console.log("x += 5:", x); // 15

x -= 3;  // x = x - 3
console.log("x -= 3:", x); // 12

x *= 2;  // x = x * 2
console.log("x *= 2:", x); // 24

x /= 4;  // x = x / 4
console.log("x /= 4:", x); // 6

x %= 4;  // x = x % 4
console.log("x %= 4:", x); // 2
```

</p>
</details>

<details>
<summary>6️⃣ Ternary Operator (Conditional Expression)</summary>
<p>

```javascript
let age = 17;
let result = (age >= 18) ? "Eligible to vote" : "Not eligible";
console.log(result); // "Not eligible"
```

</p>
</details>

<details>
<summary>7️⃣ typeof Operator (Check data types)</summary>
<p>

```javascript
let num = 42;
let str = "Hello";
let isActive = true;

console.log(typeof num);      // "number"
console.log(typeof str);      // "string"
console.log(typeof isActive); // "boolean"
console.log(typeof null);     // "object" (special case)
console.log(typeof undefined); // "undefined"
```

</p>
</details>

<details>
<summary>8️⃣ String Concatenation (+ operator)</summary>
<p>

```javascript
let firstName = "John";
let lastName = "Doe";

let fullName = firstName + " " + lastName;
console.log(fullName); // "John Doe"

let greet = "Hello " + firstName + "!";
console.log(greet); // "Hello John!"
```

</p>
</details>
