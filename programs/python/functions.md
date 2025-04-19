<details open>
<summary>Write function to find given number is even or odd.</summary>
<p>

```python
   def check_even_odd(number):
    if number % 2 == 0:
        return "Even"
    else:
        return "Odd"

# Example usage:
num = int(input("Enter a number: "))
result = check_even_odd(num)
print(f"The number {num} is {result}.")

```

</p>
</details>

<details>
<summary>Write function to convert given string to uppercase.</summary>
<p>

```python
def convert_to_uppercase(text):
    return text.upper()

# Example usage:
input_text = input("Enter a string: ")
result = convert_to_uppercase(input_text)
print(f"Uppercase version: {result}")


```

</p>
</details>
<details>
<summary>Write function to show call by value.</summary>
<p>

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

</p>
</details>

<details>
<summary>Write function to Print 1 to 10 without using loop.</summary>
<p>

```python
def print_numbers(n=1):
    if n <= 10:
        print(n)
        print_numbers(n + 1)

# Call the function
print_numbers()

```

</p>
</details>

<details>
<summary>Write function to show call by reference.</summary>
<p>

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

</p>
</details>

<details open>
<summary>Write function to return list of products.</summary>
<p>

```python
def get_products():
    products = [
        {"id": 1, "name": "Laptop", "price": 75000},
        {"id": 2, "name": "Smartphone", "price": 30000},
        {"id": 3, "name": "Headphones", "price": 2500},
        {"id": 4, "name": "Monitor", "price": 12000},
    ]
    return products

# Example usage:
product_list = get_products()
for product in product_list:
    print(product)

```

</p>
</details>


<details>
<summary>Write function to Reverse Given number.</summary>
<p>

```python
def reverse_number(n):
    reversed_num = 0
    while n > 0:
        digit = n % 10
        reversed_num = reversed_num * 10 + digit
        n = n // 10
    return reversed_num

# Example usage:
num = int(input("Enter a number: "))
result = reverse_number(num)
print(f"Reversed number: {result}")

```

</p>
</details>

<details>
<summary>Write a simple calculator.</summary>
<p>

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

# Example usage:
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))
op = input("Enter operation (+, -, *, /): ")

result = calculator(num1, num2, op)
print("Result:", result)


```

</p>
</details>
