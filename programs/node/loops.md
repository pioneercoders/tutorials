
<details open>
<summary>1️⃣ Print numbers from 1 to 10 using a for loop</summary>
<p>

```javascript
for (let i = 1; i <= 10; i++) {
    console.log(i);
}
```

</p>
</details>

<details>
<summary>2️⃣ Print numbers from 10 to 1 using a for loop</summary>
<p>

```javascript
for (let i = 10; i >= 1; i--) {
    console.log(i);
}
```

</p>
</details>

<details>
<summary>3️⃣ Print numbers from 1 to 10 using a while loop</summary>
<p>

```javascript
let i = 1;
while (i <= 10) {
    console.log(i);
    i++;
}
```

</p>
</details>

<details>
<summary>4️⃣ Print alternate numbers from 1 to 10 using a for loop</summary>
<p>

```javascript
for (let i = 1; i <= 10; i += 2) {
    console.log(i);
}
```

</p>
</details>

<details>
<summary>5️⃣ Print even numbers from 1 to 10 using a for loop</summary>
<p>

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        console.log(i);
    }
}
```

</p>
</details>

<details>
<summary>6️⃣ Print odd numbers from 1 to 10 using a for loop</summary>
<p>

```javascript
for (let i = 1; i <= 10; i++) {
    if (i % 2 !== 0) {
        console.log(i);
    }
}
```

</p>
</details>

<details>
<summary>7️⃣ Print numbers divisible by 7 between 1 and 100 using a for loop</summary>
<p>

```javascript
for (let i = 1; i <= 100; i++) {
    if (i % 7 === 0) {
        console.log(i);
    }
}
```

</p>
</details>

<details>
<summary>8️⃣ Print Fibonacci series using a for loop</summary>
<p>

```javascript
let n1 = 0, n2 = 1, nextTerm;
let count = 10;

console.log(n1);
console.log(n2);

for (let i = 2; i < count; i++) {
    nextTerm = n1 + n2;
    console.log(nextTerm);
    n1 = n2;
    n2 = nextTerm;
}
```

</p>
</details>

<details>
<summary>9️⃣ Print the sum of numbers from 1 to 10 using a for loop</summary>
<p>

```javascript
let sum = 0;
for (let i = 1; i <= 10; i++) {
    sum += i;
}
console.log("Sum:", sum);
```

</p>
</details>

<details>
<summary>🔟 Print the multiplication table of 5 using a for loop</summary>
<p>

```javascript
let num = 5;
for (let i = 1; i <= 10; i++) {
    console.log(`${num} x ${i} = ${num * i}`);
}
```

</p>
</details>

<details>
<summary>1️⃣1️⃣ Print the factorial of a number using a for loop</summary>
<p>

```javascript
let number = 5;
let factorial = 1;
for (let i = 1; i <= number; i++) {
    factorial *= i;
}
console.log("Factorial:", factorial);
```

</p>
</details>

<details>
<summary>1️⃣2️⃣ Print numbers from 1 to 10 using a while loop with condition check</summary>
<p>

```javascript
let j = 1;
while (j <= 10) {
    if (j % 2 === 0) {
        console.log("Even:", j);
    } else {
        console.log("Odd:", j);
    }
    j++;
}
```

</p>
</details>

<details>
<summary>1️⃣3️⃣ Print countdown using while loop</summary>
<p>

```javascript
let countdown = 5;
while (countdown > 0) {
    console.log("Countdown:", countdown);
    countdown--;
}
```

</p>
</details>
