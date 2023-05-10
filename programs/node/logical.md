<details open>
<summary>Write a program to find given number is Armstrong or not.</summary>
<p>

```javascript
   // program to check an Armstrong number of three digits
    let sum = 0;
    const number = prompt('Enter a three-digit positive integer: ');

    // create a temporary variable
    let temp = number;
    while (temp > 0) {
        // finding the one's digit
        let remainder = temp % 10;

        sum += remainder * remainder * remainder;

        // removing last digit from the number
        temp = parseInt(temp / 10); // convert float into integer
    }
    // check the condition
    if (sum == number) {
        console.log(`${number} is an Armstrong number`);
    }
    else {
        console.log(`${number} is not an Armstrong number.`);
    }
```

</p>
</details>

<details>
<summary>Write a program to find factorial of given number.</summary>
<p>

```javascript
   function factorial(n){
     let answer = 1;
     if (n == 0 || n == 1){
       return answer;
     }
     else if(n > 1){
       for(var i = n; i >= 1; i--){
         answer = answer * i;
       }
       return answer;
     }
     else{
       return "number has to be positive."
     }  
   }
   let n = 4;
   answer = factorial(n)
   console.log("Factorial of " + n + " : " + answer);
```

</p>
</details>
