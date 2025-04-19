<details open>
<summary>Write a program to assign a function to a variable</summary>
<p>

```python
   # Define a function
def greet(name):
    return f"Hello, {name}!"

# Assign the function to a variable
say_hello = greet

# Call the function using the new variable
print(say_hello("Krishna"))

```

</p>
</details>

<details>
<summary>Write a program to pass two arguments to a function </summary>
<p>

```python
# Define a function that takes two arguments
def add_numbers(a, b):
    return a + b

# Call the function with two values
result = add_numbers(5, 3)

# Print the result
print("The sum is:", result)


```

</p>
</details>

<details>
<summary>Write a program to pass function as argument to another function</summary>
<p>

```python

# Define a function that will be passed
def square(x):
    return x * x

# Define another function that accepts a function as argument
def apply_function(func, value):
    return func(value)

# Call apply_function and pass 'square' function and a number
result = apply_function(square, 5)

print("Result:", result)


```

</p>
</details>

<details>
<summary>Write a program to return a function from another function</summary>
<p>

```python
# Outer function
def outer_function():
    def inner_function():
        return "Hello from the inner function!"
    return inner_function  # Return the function itself, not the result

# Call the outer function and assign the returned function
my_func = outer_function()

# Call the returned function
print(my_func())

```

</p>
</details>
