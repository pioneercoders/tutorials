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
