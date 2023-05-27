<details open>
<summary>Write a program to print 1 to 10 numbers using for loop.</summary>
<p>

```javascript
  for (let i = 0; i < 10; i++) {
      console.log(i);
  }
```

</p>
</details>

<details>
<summary>Write a program to print 10 to 1 numbers using for loop.</summary>
<p>

```javascript
  for (let i = 10; i > 0; i--) {
    console.log(i);
  }
```

</p>
</details>

<details>
<summary>Write a program to print 1 to 10 numbers using while loop.</summary>
<p>

```javascript
  var i = 0
  while (i < 10) {
      console.log(i);
      i++;
  }
```

</p>
</details>

<details>
<summary>Write a program to print alternatvie number between 1 to 10 numbers using for loop.</summary>
<p>

```javascript
  for (let i = 0; i < 10; i = i + 2) {
      console.log(i);
  }
```

</p>
</details>

<details>
<summary>Write a program to print even number between 1 to 10 numbers using for loop.</summary>
<p>

```javascript
  for (let i = 0; i < 10; i++) {
      if(i%2 == 0){         
          console.log(i);
      }
  }
```

</p>
</details>

<details>
<summary>Write a program to print odd number between 1 to 10 numbers using for loop.</summary>
<p>

```javascript
  for (let i = 0; i < 10; i++) {
      if(i%2 != 0){         
          console.log(i);
      }
  }
```

</p>
</details>

<details>
<summary>Write a program to print number divisible by 7  between 1 to 100 numbers using for loop.</summary>
<p>

```javascript
  for (let i = 0; i < 100; i++) {
      if(i%7 == 0){         
          console.log(i);
      }
  }
```

</p>
</details>

<details>
<summary>Write a program to print Fibancci serious using for loop.</summary>
<p>

```javascript
  let n1=0;
  let n2=1;
  let n3=0;
  var count=10;
  console.log(n1,n2);
  for( let i=1;i<=count;i++){
      n1+n2=n3;
     console.log(n3)  
       n1=n2;
       n2=n3;
  }
```
                            
</p>
</details>
