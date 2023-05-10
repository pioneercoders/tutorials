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
