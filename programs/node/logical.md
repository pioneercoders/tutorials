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

<details>
<summary>Write a program to check if the string is palindrome or not.</summary>
<p>

```javascript
   // program to check if the string is palindrome or not

   function checkPalindrome(string) {

       // find the length of a string
       const len = string.length;

       // loop through half of the string
       for (let i = 0; i < len / 2; i++) {

           // check if first and last string are same
           if (string[i] !== string[len - 1 - i]) {
               return 'It is not a palindrome';
           }
       }
       return 'It is a palindrome';
   }

   // take input
   const string = prompt('Enter a string: ');

   // call the function
   const value = checkPalindrome(string);

   console.log(value);
```

</p>
</details>

<details>
<summary>Write a program to print starpattern.</summary>
<p>

```javascript
   let n = 5;
let string = "";
for (let i = 1; i <= n; i++) {
  // printing spaces
  for (let j = 0; j < n - i; j++) {
    string += " ";
  }
  // printing star
  for (let k = 0; k < i; k++) {
    string += "*";
  }
  string += "\n";
}
console.log(string);
```

</p>
</details>
