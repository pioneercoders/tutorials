<details open>
<summary>1️⃣ Assign a function to a variable</summary>

```python
# Define a function
def greet(name):
    return f"Hello, {name}!"

# Assign the function to a variable
say_hello = greet

# Call the function using the new variable
print(say_hello("Krishna"))
```
</details>

<details>
<summary>2️⃣ Pass two arguments to a function</summary>

```python
# Define a function that takes two arguments
def add_numbers(a, b):
    return a + b

# Call the function with two values
result = add_numbers(5, 3)

# Print the result
print("The sum is:", result)
```
</details>

<details>
<summary>3️⃣ Pass a function as an argument</summary>

```python
# Define a function to be passed
def square(x):
    return x * x

# Define a function that takes another function as argument
def apply_function(func, value):
    return func(value)

# Call with square
result = apply_function(square, 5)

print("Result:", result)
```
</details>

<details>
<summary>4️⃣ Return a function from another function</summary>

```python
def outer_function():
    def inner_function():
        return "Hello from the inner function!"
    return inner_function

my_func = outer_function()
print(my_func())
```
</details>

<details>
<summary>5️⃣ Closure in Python</summary>

```python
def outer(x):
    def inner(y):
        return x + y
    return inner

add_10 = outer(10)
print(add_10(5))  # Output: 15
```
</details>

<details>
<summary>6️⃣ Lambda function</summary>

```python
# Define a lambda function
square = lambda x: x * x

# Use the lambda function
print("Square of 4 is:", square(4))
```
</details>

<details>
<summary>7️⃣ Lambda inside a map()</summary>

```python
numbers = [1, 2, 3, 4]
squares = list(map(lambda x: x ** 2, numbers))
print("Squares:", squares)
```
</details>

<details>
<summary>8️⃣ Lambda inside a filter()</summary>

```python
numbers = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda x: x % 2 == 0, numbers))
print("Even numbers:", evens)
```
</details>

<details>
<summary>9️⃣ Decorator (without arguments)</summary>

```python
def decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@decorator
def say_hello():
    print("Hello!")

say_hello()
```
</details>

<details>
<summary>🔟 Decorator with arguments</summary>

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        print("Arguments received:", args)
        return func(*args, **kwargs)
    return wrapper

@decorator
def greet(name):
    print("Hello", name)

greet("Alice")
```
</details>

<details>
<summary>1️⃣1️⃣ Function with default arguments</summary>

```python
def greet(name="Guest"):
    print(f"Hello, {name}!")

greet()
greet("Alice")
```
</details>

<details>
<summary>1️⃣2️⃣ Recursive function (factorial)</summary>

```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

print("Factorial of 5 is:", factorial(5))
```
</details>

<details>
<summary>1️⃣3️⃣ Variable number of arguments using *args</summary>

```python
def add_all(*args):
    total = 0
    for num in args:
        total += num
    return total

print("Sum:", add_all(1, 2, 3, 4))
```
</details>

<details>
<summary>1️⃣4️⃣ Variable keyword arguments using **kwargs</summary>

```python
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=25, city="Wonderland")
```
</details>
