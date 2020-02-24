<h4> Functions</h4>
A function is a block of code which deals with some specific functionality defined once and called once/multiple times.

```python
def greet(name):
	print("Hello, Mr."+ name + " Welcome to Pioneer Coders!")

greet("Krishna") # funciton calling.

def add(x,y):
  result =  x + y;
  return result;
sum = add(10,20)
printf(sum)
```

```python
def cube(num):
    """Return the cube of the input number."""
    cube_num = num ** 3  # Could also use pow(num, 3)
    return cube_num

print(f"0 cubed is {cube(0)}")
print(f"2 cubed is {cube(2)}")
```

<h4> Scope and Lifetime of variables</h4>
The lifetime of variables inside a function is as long as the function executes. They are destroyed once we return from the function.

<details>
    <summary>Write a function for converting temperatures from Celsius to Fahrenheit and vice versa </summary>
    <p>

```python
def convert_cel_to_far(temp_cel):
    """Return the Celsius temperature temp_cel converted to Fahrenheit."""
    temp_far = temp_cel * (9 / 5) + 32
    return temp_far


def convert_far_to_cel(temp_far):
    """Return the Fahrenheit temperature temp_far converted to Celsius."""
    temp_cel = (temp_far - 32) * (5 / 9)
    return temp_cel


# Prompt the user to input a Fahrenheit temperature.
temp_far = input("Enter a temperature in degrees F: ")

# Convert the temperature to Celsius.
# Note that `temp_far` must be converted to a `float`
# since `input()` returns a string.
temp_cel = convert_far_to_cel(float(temp_far))

# Display the converted temperature
print(f"{temp_far} degrees F = {temp_cel:.2f} degrees C")

# You could also use `round()` instead of the formatting mini-language:
# print(f"{temp_far} degrees F = {round(temp_cel, 2)} degrees C"")

# Prompt the user to input a Celsius temperature.
temp_cel = input("\nEnter a temperature in degrees C: ")

# Convert the temperature to Fahrenheit.
temp_far = convert_cel_to_far(float(temp_cel))

# Display the converted temperature
print(f"{temp_cel} degrees C = {temp_far:.2f} degrees F")
```
</p>
</details>

<details>
    <summary>Write a program to calculate simple interest.</summary>
    <p>
	
```python
def simple_interest(principal, no_of_years, rate_of_interest):
    si = (principal * no_of_years * rate_of_interest) / 100
    return si

P = float(input("Enter the principal amount : "))
N = float(input("Enter the number of years : "))
R = float(input("Enter the rate of interest : "))
interest_amount = simple_interest(P, N, R)
print("Simple interest : {}".format(interest_amount))
```
</p>
</details>

<details>
    <summary>Write a program to calculate Compound Interest.</summary>
    <p>
	
```python
def compound_interest(principle, rate, no_of_years):
    result = principle * (pow((1 + rate / 100), no_of_years))
    return result

p = float(input("Enter the principal amount: "))
r = float(input("Enter the interest rate: "))
t = float(input("Enter the time in years: "))

amount = compound_interest(p, r, t)
interest = amount - p
print("Compound amount is %.2f" % amount)
print("Compound interest is %.2f" % interest)
```
</p>
</details>