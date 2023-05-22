<details open>
<summary>Write a program to sort a array of numbers.</summary>
<p>

```javascript
   for (var i = 1; i < Arr.length; i++) {
    for (var j = 0; j < i; j++) {
        if (Arr[i] < Arr[j]) {
            var x = Arr[i];
            Arr[i] = Arr[j];
            Arr[j] = x;
        }
    }
  }

  var arr = [1, 7, 2, 8, 3, 4, 5, 0, 9];
  console.log(arr);

```

</p>
</details>

<details open>
<summary>Write a program to sort a array of numbers.</summary>
<p>

```javascript
   function bubbleSort(arr) {
    const length = arr.length;
  
    for (let i = 0; i < length - 1; i++) {
      // Last i elements are already in place
      for (let j = 0; j < length - 1 - i; j++) {
        // Compare adjacent elements
        if (arr[j] > arr[j + 1]) {
          // Swap the elements
          [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
        }
      }
    }
  
    return arr;
  }
  
  // Example usage
  const num = [24, 34, 22, 16, 27, 14, 93];
  console.log("Original array: ", num);
  
  const sortedNumbers = bubbleSort(num);
  console.log("Sorted array: ", sortedNumbers);
  

```

</p>
</details>

