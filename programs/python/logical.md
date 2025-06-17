<details open>
<summary>1️⃣ Write a program to check if a number is an Armstrong Number.</summary>

```python
# Function to check Armstrong number
def is_armstrong(num):
    digits = str(num)
    power = len(digits)
    total = 0
    for digit in digits:
        total += int(digit) ** power
    return num == total

# Example usage
num = 153
if is_armstrong(num):
    print(f"{num} is an Armstrong number.")
else:
    print(f"{num} is not an Armstrong number.")
```
</details>

<details>
<summary>2️⃣ Write a program to calculate the Factorial of a given number.</summary>

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
</details>

<details>
<summary>3️⃣ Write a program to check if a string or number is a Palindrome.</summary>

```python
# Function to check palindrome
def is_palindrome(s):
    s = str(s)
    return s == s[::-1]

# Example usage
value = "madam"
if is_palindrome(value):
    print(f"'{value}' is a palindrome.")
else:
    print(f"'{value}' is not a palindrome.")
```
</details>

<details>
<summary>4️⃣ Write a program to print a Star Pattern (Right-Angled Triangle).</summary>

```python
rows = 5
for i in range(1, rows + 1):
    print("*" * i)
```
</details>

<details>
<summary>5️⃣ Write a program to find the Sum of Digits of a Number.</summary>

```python
num = 1234
sum_digits = 0
temp = num
while temp > 0:
    sum_digits += temp % 10
    temp //= 10

print(f"Sum of digits of {num} is: {sum_digits}")
```
</details>

<details>
<summary>6️⃣ Write a program to Reverse a Number.</summary>

```python
num = 1234
reversed_num = 0
temp = num
while temp > 0:
    digit = temp % 10
    reversed_num = reversed_num * 10 + digit
    temp //= 10

print(f"Reversed number of {num} is: {reversed_num}")
```
</details>

<details>
<summary>7️⃣ Write a program to check if a number is Prime.</summary>

```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n**0.5)+1):
        if n % i == 0:
            return False
    return True

# Example usage
num = 29
if is_prime(num):
    print(f"{num} is a prime number.")
else:
    print(f"{num} is not a prime number.")
```
</details>

<details>
<summary>8️⃣ Write a program to generate the Fibonacci Series up to N terms.</summary>

```python
n = 10
a, b = 0, 1
print("Fibonacci Series:")
for _ in range(n):
    print(a, end=" ")
    a, b = b, a + b
```
</details>

<details>
<summary>9️⃣ Write a program to find the GCD (Greatest Common Divisor) of two numbers.</summary>

```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

# Example usage
x, y = 48, 18
print(f"GCD of {x} and {y} is: {gcd(x, y)}")
```
</details>

<details>
<summary>🔟 Write a program to find the LCM (Least Common Multiple) of two numbers.</summary>

```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

def lcm(a, b):
    return abs(a * b) // gcd(a, b)

# Example usage
x, y = 4, 6
print(f"LCM of {x} and {y} is: {lcm(x, y)}")
```
</details>
