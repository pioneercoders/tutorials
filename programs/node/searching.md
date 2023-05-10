<details open>
<summary>Write a program to find a element using linear search.</summary>
<p>

```javascript
   function linearSearch(arr, key) {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === key) {
            return i
        }
    }
    return -1
  }

  var arr = [1, 7, 2, 8, 3, 4, 5, 0, 9];
  var result = linearSearch(arr, 9)
  console.log(result);
```

</p>
</details>
