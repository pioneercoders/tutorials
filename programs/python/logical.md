<details open>
<summary>Write programs to print Armstrong Number .</summary>
<p>

```python
  # Function to check Armstrong number
def is_armstrong(num):
    digits = str(num)
    power = len(digits)
    total = sum(int(digit) ** power for digit in digits)
    return num == total

# Example usage
num = 153
if is_armstrong(num):
    print(f"{num} is an Armstrong number.")
else:
    print(f"{num} is not an Armstrong number.")
 
```

</p>
</details>

<details>
<summary>Write programs to print Factorial of given number .</summary>
<p>

```python

# Function to calculate factorial
def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

# Example usage
num = 5
print(f"Factorial of {num} is: {factorial(num)}")

```

</p>
</details>

<details>
<summary>Write programs to check Palindrome .</summary>
<p>

```python
# Function to check if input is a palindrome
def is_palindrome(s):
    s = str(s)  # Convert to string if it's a number
    return s == s[::-1]

# Example usage
value = "madam"
if is_palindrome(value):
    print(f"'{value}' is a palindrome.")
else:
    print(f"'{value}' is not a palindrome.")

```

</p>
</details>

<details>
<summary>Write programs to print StarPattern.</summary>
<p>

```python
rows = 5
for i in range(1, rows + 1):
    print("*" * i)


```

</p>
</details>
