<details open>
<summary>Write a program to print Hello World.</summary>
<p>

```python
for i in range(1, 11):
    print(i)
```
</p>
</details>

<details open>
<summary>Write a program to print odd numbers for given number.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Loop to print odd numbers
for i in range(1, num + 1):
    if i % 2 != 0:
        print(i)
```
</p>
</details>

<details open>
<summary>Write a program to print even numbers for given number.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Loop to print even numbers
for i in range(1, num + 1):
    if i % 2 == 0:
        print(i)
```
</p>
</details>

<details open>
<summary>Write a program to Print Numbers from 1 to a Given Number using while loop.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Initialize counter
i = 1

# Loop to print numbers
while i <= num:
    print(i)
    i += 1

```
</p>
</details>
<details open>
<summary>Write a program to Print Even Numbers to a Given Number using while loop.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Start from 1
i = 1

# Loop to print even numbers
while i <= num:
    if i % 2 == 0:
        print(i)
    i += 1
```
</p>
</details>

<details open>
<summary>Write a program to Print Odd Numbers to a Given Number using while loop.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Start from 1
i = 1

# Loop to print odd numbers
while i <= num:
    if i % 2 != 0:
        print(i)
    i += 1
```
</p>
</details>

<details open>
<summary>Write a program to Print Numbers from 1 to a Given Number using do-while loop. </summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Initialize counter
i = 1

# Simulated do-while loop
while True:
    print(i)
    i += 1
    if i > num:
        break
```
</p>
</details>

<details open>
<summary>Write a program to Print Even Numbers to a Given Number using do-while loop. </summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Initialize counter
i = 1

# Simulated do-while loop
while True:
    if i % 2 == 0:
        print(i)
    i += 1
    if i > num:
        break
```
</p>
</details>


<details open>
<summary>Write a program to Print Odd Numbers to a Given Number using do-while loop.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Initialize counter
i = 1

# Simulated do-while loop
while True:
    if i % 2 != 0:
        print(i)
    i += 1
    if i > num:
        break

```
</p>
</details>

<details open>
<summary>Write a program to print given number is amstrong.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Store the original number
original = num

# Count the number of digits
n = len(str(num))

# Calculate sum of the nth power of each digit
sum_of_powers = 0
temp = num
while temp > 0:
    digit = temp % 10
    sum_of_powers += digit ** n
    temp //= 10

# Check if the number is an Armstrong number
if original == sum_of_powers:
    print(f"{original} is an Armstrong number.")
else:
    print(f"{original} is not an Armstrong number.")

```
</p>
</details>

<details open>
<summary>Write a program to print multiplication table for given number.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))
limit = int(input("Enter the limit for the multiplication table: "))

# Loop to print the multiplication table
for i in range(1, limit + 1):
    print(f"{num} x {i} = {num * i}")
```
</p>
</details>

<details open>
<summary>Write a program to print sum of individual digits for given number.</summary>
<p>

```python
# Input from user
num = int(input("Enter a number: "))

# Variable to store the sum of digits
sum_of_digits = 0

# Loop to extract and add each digit
while num > 0:
    digit = num % 10
    sum_of_digits += digit
    num //= 10

# Print the result
print(f"The sum of the digits is: {sum_of_digits}")
```
</p>
</details>
<details open>
<summary>Write a program to print Fibnacci Series.</summary>
<p>

```python
# Input from user
terms = int(input("Enter the number of terms: "))

# First two terms of the Fibonacci series
a, b = 0, 1

# Print the Fibonacci series
print("Fibonacci Series:")
for _ in range(terms):
    print(a, end=" ")
    a, b = b, a + b  # Update a and b for the next term
```
</p>
</details>

<details open>
<summary>Write a program to print Pascal Triangle.</summary>
<p>

```python
# Program to print Pascal's Triangle up to a given number of rows

# Input from user
rows = int(input("Enter the number of rows: "))

# Function to print Pascal's Triangle
def print_pascals_triangle(n):
    for i in range(n):
        # Print leading spaces for alignment
        print(" " * (n - i - 1), end="")

        # Calculate and print each number in the row
        num = 1
        for j in range(i + 1):
            print(num, end=" ")

            # Update num to the next value in Pascal's Triangle
            num = num * (i - j) // (j + 1)

        print()  # Move to the next line after each row

# Print Pascal's Triangle
print_pascals_triangle(rows)
```
</p>
</details>

<details open>
<summary>Write a program to find HCF..</summary>
<p>

```python
# Input from user
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))

# Find the smaller number
smaller = min(num1, num2)

# Initialize hcf
hcf = 1

# Loop to find HCF
for i in range(1, smaller + 1):
    if num1 % i == 0 and num2 % i == 0:
        hcf = i

# Print the result
print(f"The HCF of {num1} and {num2} is: {hcf}")
```
</p>
</details>

t_pascals_triangle(rows)
```
</p>
</details>

<details open>
<summary>Write the program to print the following series 3 33 333 3333 33333 333333.</summary>
<p>

```python
# Input: Number of terms
terms = int(input("Enter the number of terms: "))

# Initialize the number
num = 3

# Print the series
for i in range(terms):
    print(num, end=" ")
    num = num * 10 + 3

```
</p>
</details>

<details open>
<summary>Write the program to print Arithmetic Progression.</summary>
<p>

```python

# Input from user
a = int(input("Enter the first term (a): "))
d = int(input("Enter the common difference (d): "))
n = int(input("Enter the number of terms (n): "))

# Print the AP series
print("Arithmetic Progression:")
for i in range(n):
    term = a + i * d
    print(term, end=" ")
```
</p>
</details>

<details open>
<summary>Write the program to print Geometric Progression.</summary>
<p>

```python
# Input from user
a = int(input("Enter the first term (a): "))
r = int(input("Enter the common ratio (r): "))
n = int(input("Enter the number of terms (n): "))

# Print the GP series
print("Geometric Progression:")
for i in range(n):
    term = a * (r ** i)
    print(term, end=" ")
```
</p>
</details>
