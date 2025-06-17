<details open>
<summary>1️⃣ Linear Search (Search element one-by-one).</summary>
<p>

```javascript
function linearSearch(arr, key) {
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === key) {
      return i; // Return the index of found element
    }
  }
  return -1; // Element not found
}

const arr = [1, 7, 2, 8, 3, 4, 5, 0, 9];
const key = 9;

const index = linearSearch(arr, key);
if (index !== -1) {
  console.log(`Element ${key} found at index ${index}`);
} else {
  console.log(`Element ${key} not found`);
}
```

</p>
</details>

<details>
<summary>2️⃣ Linear Search for all occurrences (Find all matching values).</summary>
<p>

```javascript
function findAllOccurrences(arr, key) {
  const indices = [];

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] === key) {
      indices.push(i);
    }
  }

  return indices;
}

const values = [4, 2, 4, 7, 4, 9, 1];
const search = 4;

const result = findAllOccurrences(values, search);
if (result.length > 0) {
  console.log(`Element ${search} found at indices: ${result}`);
} else {
  console.log(`Element ${search} not found`);
}
```

</p>
</details>

<details>
<summary>3️⃣ Binary Search (For sorted arrays only).</summary>
<p>

```javascript
function binarySearch(arr, key) {
  let low = 0;
  let high = arr.length - 1;

  while (low <= high) {
    let mid = Math.floor((low + high) / 2);

    if (arr[mid] === key) {
      return mid; // Key found
    } else if (arr[mid] < key) {
      low = mid + 1; // Search right half
    } else {
      high = mid - 1; // Search left half
    }
  }

  return -1; // Key not found
}

const sortedArr = [1, 3, 5, 7, 9, 11, 13];
const keyToFind = 7;

const index = binarySearch(sortedArr, keyToFind);
if (index !== -1) {
  console.log(`Element ${keyToFind} found at index ${index}`);
} else {
  console.log(`Element ${keyToFind} not found`);
}
```

</p>
</details>

<details>
<summary>4️⃣ Linear Search in a 2D Array (Matrix Search).</summary>
<p>

```javascript
function searchMatrix(matrix, key) {
  for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix[i].length; j++) {
      if (matrix[i][j] === key) {
        return { row: i, col: j };
      }
    }
  }
  return null;
}

const matrix = [
  [3, 5, 7],
  [8, 10, 12],
  [15, 18, 21]
];

const key = 10;
const result = searchMatrix(matrix, key);

if (result) {
  console.log(`Element ${key} found at row ${result.row}, column ${result.col}`);
} else {
  console.log(`Element ${key} not found in matrix`);
}
```

</p>
</details>
