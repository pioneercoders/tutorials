<details open>
<summary>1️⃣ Sum all elements in an array</summary>
<p>

```javascript
function sumArray(arr) {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}

const data = [10, 34, 56, 78];
console.log(sumArray(data)); // 178
```

</p>
</details>

<details>
<summary>2️⃣ Get even elements in an array</summary>
<p>

```javascript
function getEvenNum(arr) {
    const evenNumbersArr = [];
    for (let index = 0; index < arr.length; index++) {
        if (arr[index] % 2 === 0) {
            evenNumbersArr.push(arr[index]);
        }
    }
    return evenNumbersArr;
}

const data = [10, 34, 56, 78, 11, 9];
console.log(getEvenNum(data)); // [10, 34, 56, 78]
```

</p>
</details>

<details>
<summary>3️⃣ Get elements at even indices</summary>
<p>

```javascript
function getElementAtEvenIndex(arr) {
    const numbersArr = [];
    for (let index = 0; index < arr.length; index++) {
        if (index % 2 === 0) {
            numbersArr.push(arr[index]);
        }
    }
    return numbersArr;
}

const data = [10, 34, 56, 78, 11, 9];
console.log(getElementAtEvenIndex(data)); // [10, 56, 11]
```

</p>
</details>

<details>
<summary>4️⃣ Get duplicate elements in array</summary>
<p>

```javascript
function getDuplicate(arr) {
    const duplicateArr = [];
    const seen = new Set();
    const added = new Set();

    for (let index = 0; index < arr.length; index++) {
        if (seen.has(arr[index]) && !added.has(arr[index])) {
            duplicateArr.push(arr[index]);
            added.add(arr[index]);
        } else {
            seen.add(arr[index]);
        }
    }

    return duplicateArr;
}

const data = [10, 34, 56, 78, 11, 9, 9, 11];
console.log(getDuplicate(data)); // [9, 11]
```

</p>
</details>

<details>
<summary>5️⃣ Get max element in array</summary>
<p>

```javascript
function largestNumInArr(arr) {
    let max = arr[0];
    for (let index = 1; index < arr.length; index++) {
        if (arr[index] > max) {
            max = arr[index];
        }
    }
    return max;
}

const data = [10, 34, 56, 78, 11, 9, 9, 11];
console.log(largestNumInArr(data)); // 78
```

</p>
</details>

<details>
<summary>6️⃣ Sort elements in array (ascending)</summary>
<p>

```javascript
function sortArr(arr) {
    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i] > arr[j]) {
                const temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr;
}

const data = [10, 34, 56, 78, 11, 9, 9, 11];
console.log(sortArr(data)); // [9, 9, 10, 11, 11, 34, 56, 78]
```

</p>
</details>

<details>
<summary>7️⃣ Count number of 0s in array</summary>
<p>

```javascript
function getNumberOfZeros(arr) {
    let count = 0;
    for (let index = 0; index < arr.length; index++) {
        if (arr[index] === 0) {
            count++;
        }
    }
    return count;
}

const data = [10, 34, 56, 78, 11, 9, 0, 30, 0, 5, 0];
console.log(getNumberOfZeros(data)); // 3
```

</p>
</details>

<details>
<summary>8️⃣ Remove duplicates from array</summary>
<p>

```javascript
function removeDuplicates(arr) {
    return [...new Set(arr)];
}

const data = [10, 20, 30, 10, 20, 40];
console.log(removeDuplicates(data)); // [10, 20, 30, 40]
```

</p>
</details>

<details>
<summary>9️⃣ Reverse an array</summary>
<p>

```javascript
function reverseArray(arr) {
    return arr.slice().reverse();
}

const data = [10, 20, 30, 40];
console.log(reverseArray(data)); // [40, 30, 20, 10]
```

</p>
</details>

<details>
<summary>🔟 Find index of an element in array</summary>
<p>

```javascript
function findIndex(arr, value) {
    return arr.indexOf(value);
}

const data = [5, 10, 15, 20];
console.log(findIndex(data, 15)); // 2
```

</p>
</details>

<details>
<summary>1️⃣1️⃣ Check if all elements are positive</summary>
<p>

```javascript
function areAllPositive(arr) {
    return arr.every(num => num > 0);
}

console.log(areAllPositive([1, 2, 3]));   // true
console.log(areAllPositive([1, -2, 3]));  // false
```

</p>
</details>

<details>
<summary>1️⃣2️⃣ Filter out negative numbers from array</summary>
<p>

```javascript
function filterNegatives(arr) {
    return arr.filter(num => num >= 0);
}

const data = [-1, 2, -3, 4, 0];
console.log(filterNegatives(data)); // [2, 4, 0]
```

</p>
</details>

<details>
<summary>1️⃣3️⃣ Find second largest number in array</summary>
<p>

```javascript
function secondLargest(arr) {
    const uniqueSorted = [...new Set(arr)].sort((a, b) => b - a);
    return uniqueSorted[1] || null;
}

console.log(secondLargest([10, 5, 20, 20, 15])); // 15
```

</p>
</details>

<details>
<summary>1️⃣4️⃣ Merge two arrays and sort</summary>
<p>

```javascript
function mergeAndSort(arr1, arr2) {
    return [...arr1, ...arr2].sort((a, b) => a - b);
}

console.log(mergeAndSort([3, 5, 1], [4, 2, 6])); // [1, 2, 3, 4, 5, 6]
```

</p>
</details>
