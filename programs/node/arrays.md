<details open>
<summary open>Write a program to sum all the elements in array.</summary>
<p>

```javascript

function sumArray(arr){
  let sum=0;
  for(var i=0;i<arr.length;i++){
      sum+=arr[i];
  }
  return sum;
}
 var data = [10,34,56,78];
 var finalSum = sumArray(data);
 console.log(finalSum);
```

</p>
</details> 
