<details open>
<summary>Write a function to add two numbers.</summary>
<p>

```javascript
    function add(x, y) {
      var z = x + y;
      return z;
    }
    let result = add(5, 8);
    console.log(result);
    let result1 = add(9, 10);
    console.log(result1);
```

</p>
</details>

<details>
<summary>Write a function to tell given number is even or not.</summary>
<p>

```javascript
    function isEven(x) {
      var result = x%2 == 0;
      return result;
    }
    let r1 = add(5, 8);
    console.log(r1);
    let r2 = add(9, 10);
    console.log(r2);
```

</p>
</details>

<details>
<summary>Write a function to multiply each element in a array with 2 and return.</summary>
<p>

```javascript
    function multiplyWith2(arr) {
      for(var index=0;i<arr.length;i++){
            arr[i] = arr[i] * 2;
      }
      return arr;
    }
    var arr = [2,5,9,12];                                     
    let result = multiplyWith2(arr);
    console.log(result);
```

</p>
</details>

<details >
<summary>Write a function to find max element between two numbers.</summary>
<p>

```javascript
    function max(x, y) {
      let max = x;
      if(x<y){
         max = y;
      }
      return max;
    }
    let result = max(8, 5);
    console.log(result);
    let result1 = max(9, 10);
    console.log(result1);
```

</p>
</details>

<details >
<summary>Write a function to print 1 to 10 numbers with out using loop.</summary>
<p>

```javascript
    function display(x) {
     let i=0;
     if(i<=x){
      return i; 
        i++;
     }
    }
   let x=10;
   let result=display(x);
   console.log(result);
```

</p>
</details>
