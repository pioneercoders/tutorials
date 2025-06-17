<details open>
<summary>1️⃣ Write a program for Matrix Multiplication.</summary>
<p>

```javascript
// Multiply two 2x2 matrices
let r = 2;
let c = 2;
const mA = [[1, 2], [3, 4]];
const mB = [[1, -1], [2, -2]];
const mC = [[], []];

for (let i = 0; i < r; i++) {
    for (let j = 0; j < c; j++) {
        mC[i][j] = 0;
        for (let k = 0; k < c; k++) {
            mC[i][j] += mA[i][k] * mB[k][j];
        }
    }
}

console.log("Matrix Multiplication Result:");
console.log(mC); // Output: [[5, -5], [11, -11]]
```

</p>
</details>

<details>
<summary>2️⃣ Write a program for Matrix Addition.</summary>
<p>

```javascript
// Add two 2x2 matrices
let A = [[1, 2], [3, 4]];
let B = [[5, 6], [7, 8]];
let sum = [[], []];

for (let i = 0; i < 2; i++) {
    for (let j = 0; j < 2; j++) {
        sum[i][j] = A[i][j] + B[i][j];
    }
}

console.log("Matrix Addition Result:");
console.log(sum); // [[6, 8], [10, 12]]
```

</p>
</details>

<details>
<summary>3️⃣ Write a program for Matrix Subtraction.</summary>
<p>

```javascript
// Subtract two 2x2 matrices
let A = [[9, 8], [7, 6]];
let B = [[1, 2], [3, 4]];
let diff = [[], []];

for (let i = 0; i < 2; i++) {
    for (let j = 0; j < 2; j++) {
        diff[i][j] = A[i][j] - B[i][j];
    }
}

console.log("Matrix Subtraction Result:");
console.log(diff); // [[8, 6], [4, 2]]
```

</p>
</details>

<details>
<summary>4️⃣ Write a program to find Transpose of a Matrix.</summary>
<p>

```javascript
// Transpose of a 2x3 matrix
let matrix = [
    [1, 2, 3],
    [4, 5, 6]
];

let rows = 2;
let cols = 3;
let transpose = [[], [], []];

for (let i = 0; i < cols; i++) {
    for (let j = 0; j < rows; j++) {
        transpose[i][j] = matrix[j][i];
    }
}

console.log("Transpose of Matrix:");
console.log(transpose);
// Output:
// [
//   [1, 4],
//   [2, 5],
//   [3, 6]
// ]
```

</p>
</details>

<details>
<summary>5️⃣ Write a program to check if a matrix is an Identity Matrix.</summary>
<p>

```javascript
// Identity matrix check for 3x3
let identity = [
    [1, 0, 0],
    [0, 1, 0],
    [0, 0, 1]
];

let isIdentity = true;

for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        if ((i === j && identity[i][j] !== 1) || (i !== j && identity[i][j] !== 0)) {
            isIdentity = false;
        }
    }
}

console.log("Is Identity Matrix?", isIdentity); // true
```

</p>
</details>

<details>
<summary>6️⃣ Write a program to calculate the Sum of Diagonal Elements of a Square Matrix.</summary>
<p>

```javascript
// Diagonal sum of 3x3 matrix
let mat = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

let mainDiag = 0;
let secDiag = 0;

for (let i = 0; i < 3; i++) {
    mainDiag += mat[i][i]; // top-left to bottom-right
    secDiag += mat[i][2 - i]; // top-right to bottom-left
}

console.log("Main Diagonal Sum:", mainDiag); // 15
console.log("Secondary Diagonal Sum:", secDiag); // 15
```

</p>
</details>
