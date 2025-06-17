<details open>
<summary>1️⃣ Write a function to check whether a number is even or odd.</summary>

```python
def check_even_odd(number):
    if number % 2 == 0:
        return "Even"
    else:
        return "Odd"

# Example usage
num = int(input("Enter a number: "))
result = check_even_odd(num)
print(f"The number {num} is {result}.")
```
</details>

<details>
<summary>2️⃣ Write a function to convert a given string to uppercase.</summary>

```python
def convert_to_uppercase(text):
    return text.upper()

# Example usage
input_text = input("Enter a string: ")
result = convert_to_uppercase(input_text)
print(f"Uppercase version: {result}")
```
</details>

<details>
<summary>3️⃣ Write a function to demonstrate call by value behavior in Python.</summary>

```python
def modify_value(x):
    print(f"Inside function before change: x = {x}")
    x = x + 10
    print(f"Inside function after change: x = {x}")

# Example usage
num = 20
print(f"Before function call: num = {num}")
modify_value(num)
print(f"After function call: num = {num}")
```
</details>

<details>
<summary>4️⃣ Write a recursive function to print numbers from 1 to 10 without using a loop.</summary>

```python
def print_numbers(n=1):
    if n <= 10:
        print(n)
        print_numbers(n + 1)

# Call the function
print_numbers()
```
</details>

<details>
<summary>5️⃣ Write a function to demonstrate call by reference behavior in Python.</summary>

```python
def modify_list(my_list):
    print(f"Inside function before change: {my_list}")
    my_list.append(100)
    print(f"Inside function after change: {my_list}")

# Example usage
numbers = [1, 2, 3]
print(f"Before function call: {numbers}")
modify_list(numbers)
print(f"After function call: {numbers}")
```
</details>

<details>
<summary>6️⃣ Write a function to return a list of products.</summary>

```python
def get_products():
    products = [
        {"id": 1, "name": "Laptop", "price": 75000},
        {"id": 2, "name": "Smartphone", "price": 30000},
        {"id": 3, "name": "Headphones", "price": 2500},
        {"id": 4, "name": "Monitor", "price": 12000},
    ]
    return products

# Example usage
product_list = get_products()
for product in product_list:
    print(product)
```
</details>

<details>
<summary>7️⃣ Write a function to reverse a given number.</summary>

```python
def reverse_number(n):
    reversed_num = 0
    while n > 0:
        digit = n % 10
        reversed_num = reversed_num * 10 + digit
        n = n // 10
    return reversed_num

# Example usage
num = int(input("Enter a number: "))
result = reverse_number(num)
print(f"Reversed number: {result}")
```
</details>

<details>
<summary>8️⃣ Write a function to implement a simple calculator.</summary>

```python
def calculator(a, b, operation):
    if operation == "+":
        return a + b
    elif operation == "-":
        return a - b
    elif operation == "*":
        return a * b
    elif operation == "/":
        if b == 0:
            return "Error: Division by zero"
        return a / b
    else:
        return "Invalid operation"

# Example usage
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))
op = input("Enter operation (+, -, *, /): ")
result = calculator(num1, num2, op)
print("Result:", result)
```
</details>

<details>
<summary>9️⃣ Write a function to check if a number is prime.</summary>

```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n ** 0.5) + 1):
        if n % i == 0:
            return False
    return True

# Example usage
num = int(input("Enter a number: "))
if is_prime(num):
    print(f"{num} is a prime number.")
else:
    print(f"{num} is not a prime number.")
```
</details>

<details>
<summary>🔟 Write a function to find the factorial of a number using recursion.</summary>

```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

# Example usage
num = int(input("Enter a number: "))
print(f"Factorial of {num} is: {factorial(num)}")
```
</details>

<details>
<summary>1️⃣1️⃣ Write a function to return square of a number.</summary>

```python
def square(n):
    return n * n

# Example usage
num = int(input("Enter a number: "))
print(f"Square of {num} is {square(num)}")
```
</details>

<details>
<summary>1️⃣2️⃣ Write a function to return cube of a number.</summary>

```python
def cube(n):
    return n * n * n

# Example usage
num = int(input("Enter a number: "))
print(f"Cube of {num} is {cube(num)}")
```
</details>
