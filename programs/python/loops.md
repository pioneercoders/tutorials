<details open>
<summary>1️⃣ Write a program to print Hello World 10 times.</summary>
<p>

```python
for i in range(1, 11):
    print(i)
```

</p>
</details>

<details>
<summary>2️⃣ Write a program to print odd numbers for a given number.</summary>
<p>

```python
num = int(input("Enter a number: "))
for i in range(1, num + 1):
    if i % 2 != 0:
        print(i)
```

</p>
</details>

<details>
<summary>3️⃣ Write a program to print even numbers for a given number.</summary>
<p>

```python
num = int(input("Enter a number: "))
for i in range(1, num + 1):
    if i % 2 == 0:
        print(i)
```

</p>
</details>

<details>
<summary>4️⃣ Write a program to print numbers from 1 to a given number using while loop.</summary>
<p>

```python
num = int(input("Enter a number: "))
i = 1
while i <= num:
    print(i)
    i += 1
```

</p>
</details>

<details>
<summary>5️⃣ Write a program to print even numbers to a given number using while loop.</summary>
<p>

```python
num = int(input("Enter a number: "))
i = 1
while i <= num:
    if i % 2 == 0:
        print(i)
    i += 1
```

</p>
</details>

<details>
<summary>6️⃣ Write a program to print odd numbers to a given number using while loop.</summary>
<p>

```python
num = int(input("Enter a number: "))
i = 1
while i <= num:
    if i % 2 != 0:
        print(i)
    i += 1
```

</p>
</details>

<details>
<summary>7️⃣ Write a program to print numbers from 1 to a given number using do-while loop.</summary>
<p>

```python
num = int(input("Enter a number: "))
i = 1
while True:
    print(i)
    i += 1
    if i > num:
        break
```

</p>
</details>

<details>
<summary>8️⃣ Write a program to print even numbers to a given number using do-while loop.</summary>
<p>

```python
num = int(input("Enter a number: "))
i = 1
while True:
    if i % 2 == 0:
        print(i)
    i += 1
    if i > num:
        break
```

</p>
</details>

<details>
<summary>9️⃣ Write a program to print odd numbers to a given number using do-while loop.</summary>
<p>

```python
num = int(input("Enter a number: "))
i = 1
while True:
    if i % 2 != 0:
        print(i)
    i += 1
    if i > num:
        break
```

</p>
</details>

<details>
<summary>🔟 Write a program to check if a number is Armstrong.</summary>
<p>

```python
num = int(input("Enter a number: "))
original = num
n = len(str(num))
sum_of_powers = 0
temp = num

while temp > 0:
    digit = temp % 10
    sum_of_powers += digit ** n
    temp //= 10

if original == sum_of_powers:
    print(f"{original} is an Armstrong number.")
else:
    print(f"{original} is not an Armstrong number.")
```

</p>
</details>

<details>
<summary>1️⃣1️⃣ Write a program to print multiplication table for a given number.</summary>
<p>

```python
num = int(input("Enter a number: "))
limit = int(input("Enter the limit for the multiplication table: "))

for i in range(1, limit + 1):
    print(f"{num} x {i} = {num * i}")
```

</p>
</details>

<details>
<summary>1️⃣2️⃣ Write a program to print sum of individual digits for a given number.</summary>
<p>

```python
num = int(input("Enter a number: "))
sum_of_digits = 0

while num > 0:
    digit = num % 10
    sum_of_digits += digit
    num //= 10

print(f"The sum of the digits is: {sum_of_digits}")
```

</p>
</details>

<details>
<summary>1️⃣3️⃣ Write a program to print Fibonacci Series.</summary>
<p>

```python
terms = int(input("Enter the number of terms: "))
a, b = 0, 1

print("Fibonacci Series:")
for _ in range(terms):
    print(a, end=" ")
    a, b = b, a + b
```

</p>
</details>

<details>
<summary>1️⃣4️⃣ Write a program to print Pascal's Triangle.</summary>
<p>

```python
rows = int(input("Enter the number of rows: "))

def print_pascals_triangle(n):
    for i in range(n):
        print(" " * (n - i - 1), end="")
        num = 1
        for j in range(i + 1):
            print(num, end=" ")
            num = num * (i - j) // (j + 1)
        print()

print_pascals_triangle(rows)
```

</p>
</details>

<details>
<summary>1️⃣5️⃣ Write a program to find HCF of two numbers.</summary>
<p>

```python
num1 = int(input("Enter first number: "))
num2 = int(input("Enter second number: "))
smaller = min(num1, num2)
hcf = 1

for i in range(1, smaller + 1):
    if num1 % i == 0 and num2 % i == 0:
        hcf = i

print(f"The HCF of {num1} and {num2} is: {hcf}")
```

</p>
</details>

<details>
<summary>1️⃣6️⃣ Write a program to print the series: 3 33 333 3333...</summary>
<p>

```python
terms = int(input("Enter the number of terms: "))
num = 3

for i in range(terms):
    print(num, end=" ")
    num = num * 10 + 3
```

</p>
</details>

<details>
<summary>1️⃣7️⃣ Write a program to print Arithmetic Progression.</summary>
<p>

```python
a = int(input("Enter the first term (a): "))
d = int(input("Enter the common difference (d): "))
n = int(input("Enter the number of terms (n): "))

print("Arithmetic Progression:")
for i in range(n):
    term = a + i * d
    print(term, end=" ")
```

</p>
</details>

<details>
<summary>1️⃣8️⃣ Write a program to print Geometric Progression.</summary>
<p>

```python
a = int(input("Enter the first term (a): "))
r = int(input("Enter the common ratio (r): "))
n = int(input("Enter the number of terms (n): "))

print("Geometric Progression:")
for i in range(n):
    term = a * (r ** i)
    print(term, end=" ")
```

</p>
</details>
