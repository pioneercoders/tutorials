<details open>
<summary open>Write a program to sum all the elements in array.</summary>
<p>

```javascript
function sumArray(arr) {
    let sum = 0;
    for (var i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}
var data = [10, 34, 56, 78];
var finalSum = sumArray(data);
console.log(finalSum);
```

</p>
</details> 

<details>
<summary open>Write a program to get even elements in array.</summary>
<p>

```javascript
function getEvenNum(arr) {
    let evenNumbersArr = [];
    for (index = 0; index < arr.length; index++) {
        if (arr[index] % 2 == 0) {
            evenNumbersArr.push(arr[index]);
        }
    }
    return evenNumbersArr;
}
var data = [10, 34, 56, 78, 11, 9];
var result = getEvenNum(data);
console.log(result);
```

</p>
</details> 

<details>
<summary open>Write a program to get elements at even index in array.</summary>
<p>

```javascript
function getElementAtEvenIndex(arr) {
    let numbersArr = [];
    for (index = 0; index < arr.length; index++) {
        if (index % 2 == 0) {
            numbersArr.push(arr[index]);
        }
    }
    return numbersArr;
}
var data = [10, 34, 56, 78, 11, 9];
var result = getElementAtEvenIndex(data);
console.log(result);
```

</p>
</details> 

<details>
<summary open>Write a program to get duplicate elements in array.</summary>
<p>

```javascript
function getDuplicate(arr) {
    let duplicateArr = [];
    for (var index = 0; index < arr.length; index++) {
        for (var j = index + 1; j < arr.length; j++) {
            if (arr[index] == arr[j]) {
                y = arr[index];
                duplicateArr.push(y);
            }
        }
    }
    return duplicateArr;
}
var data = [10, 34, 56, 78, 11, 9, 9, 11];
var result = getDuplicate(data);
console.log(result);
```

</p>
</details> 

<details>
<summary open>Write a program to get Max element in array.</summary>
<p>

```javascript
function largestNumInArr(arr) {
    var max = arr[0];
    for (var index = 0; index < arr.length; index++) {
        if (arr[index] > max) {
            max = arr[index];
        }
    }
    return max;
}
var data = [10, 34, 56, 78, 11, 9, 9, 11];
var result = largestNumInArr(data);
console.log(result);
```

</p>
</details> 
