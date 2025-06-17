<details open>
<summary>1️⃣ Insertion Sort: Sort an array of numbers (in-place).</summary>
<p>

```javascript
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let current = arr[i];
    let j = i - 1;

    // Shift larger elements to the right
    while (j >= 0 && arr[j] > current) {
      arr[j + 1] = arr[j];
      j--;
    }

    // Insert the current element at its correct position
    arr[j + 1] = current;
  }
  return arr;
}

// Example
let arr1 = [1, 7, 2, 8, 3, 4, 5, 0, 9];
console.log("Insertion Sort:", insertionSort(arr1)); // [0, 1, 2, 3, 4, 5, 7, 8, 9]
```

</p>
</details>

<details>
<summary>2️⃣ Bubble Sort: Sort an array of numbers by repeatedly swapping adjacent elements.</summary>
<p>

```javascript
function bubbleSort(arr) {
  const length = arr.length;

  for (let i = 0; i < length - 1; i++) {
    // Flag to detect early completion
    let swapped = false;

    for (let j = 0; j < length - 1 - i; j++) {
      // Compare adjacent elements
      if (arr[j] > arr[j + 1]) {
        // Swap the elements
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
        swapped = true;
      }
    }

    // If no swaps occurred, the array is already sorted
    if (!swapped) break;
  }

  return arr;
}

// Example
let arr2 = [24, 34, 22, 16, 27, 14, 93];
console.log("Bubble Sort:", bubbleSort(arr2)); // [14, 16, 22, 24, 27, 34, 93]
```

</p>
</details>

<details>
<summary>3️⃣ Selection Sort: Find the minimum element and put it at the beginning.</summary>
<p>

```javascript
function selectionSort(arr) {
  const n = arr.length;

  for (let i = 0; i < n - 1; i++) {
    let minIdx = i;

    // Find the index of the minimum element
    for (let j = i + 1; j < n; j++) {
      if (arr[j] < arr[minIdx]) {
        minIdx = j;
      }
    }

    // Swap if a smaller element is found
    if (minIdx !== i) {
      let temp = arr[i];
      arr[i] = arr[minIdx];
      arr[minIdx] = temp;
    }
  }

  return arr;
}

// Example
let arr3 = [29, 10, 14, 37, 13];
console.log("Selection Sort:", selectionSort(arr3)); // [10, 13, 14, 29, 37]
```

</p>
</details>

<details>
<summary>4️⃣ Sort array using manual swapping logic (simple for-loop method).</summary>
<p>

```javascript
let arr4 = [1, 7, 2, 8, 3, 4, 5, 0, 9];

// Manual nested loop for sorting (similar to insertion sort logic)
for (let i = 1; i < arr4.length; i++) {
  for (let j = 0; j < i; j++) {
    if (arr4[i] < arr4[j]) {
      // Swap elements
      let temp = arr4[i];
      arr4[i] = arr4[j];
      arr4[j] = temp;
    }
  }
}

console.log("Manual loop sort:", arr4); // [0, 1, 2, 3, 4, 5, 7, 8, 9]
```

</p>
</details>

