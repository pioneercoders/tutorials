<details open>
<summary>Write a function to count number of words in a string.</summary>
<p>

```javascript
    function countWords(str) {
      return str.split(" ").length;
    }

    let result = countWords("Hi welcome to coding krishna website.");
    console.log(result);
```

</p>
</details>

<details open>
<summary>Write a function to count number of words in a string.</summary>
<p>

```javascript
  function compareStr(str1, str2) {
    if (str1.match(str2)) {
        return true;
    } else {
        return false;
    }
  }

  let result = compareStr("codingkrishna", "codingkrishna");
  console.log(result);
```

</p>
</details>
