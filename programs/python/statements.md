<details open>
<summary>Write a program to find Simple Interst.</summary>
<p>

```python
# Simple Interest Formula: (P × R × T) / 100

principal = 1000     
rate = 5             
time = 2

simple_interest = (principal * rate * time) / 100

print("Principal:", principal)
print("Rate of Interest:", rate)
print("Time (in years):", time)
print("Simple Interest =", simple_interest)

```
</p>
</details> 

<details>
<summary open> Write a program to find Compound Interst.</summary>
<p>

```python


principal = 5000      
rate = 5               
time = 3                
n = 4              

rate = rate / 100

amount = principal * (1 + rate / n) ** (n * time)

# Calculate compound interest
compound_interest = amount - principal

# Display results
print("Principal (P):", principal)
print("Rate of Interest (%):", rate * 100)
print("Time (years):", time)
print("Compounded:", n, "times/year")
print("Total Amount (A):", round(amount, 2))
print("Compound Interest:", round(compound_interest, 2))

```
</p>
</details> 


<details>
<summary open> Write a program to find area of circle.</summary>
<p>

```python

radius = 7  # Radius of the circle

# Use value of pi
pi = 3.14159

# Calculate area
area = pi * radius * radius

# Display result
print("Radius of the circle:", radius)
print("Area of the circle:", round(area, 2))


```
</p>
</details> 


<details>
<summary open> Write a program to find average of three numbers.</summary>
<p>

```python
num1 = 10
num2 = 20
num3 = 30

total = num1 + num2 + num3
average = total / 3

print("First number:", num1)
print("Second number:", num2)
print("Third number:", num3)
print("Average of three numbers:", average)
```
</p>
</details> 

<details>
<summary open> Write a program to find Max between two numbers.</summary>
<p>

```python
a = 15
b = 25

if a > b:
    print("Maximum number is:", a)
else:
    print("Maximum number is:", b)
```
</p>
</details> 

<details>
<summary open>  Write a program to find Smallest number.</summary>
<p>

```python
x = 12
y = 7
z = 15

if x < y and x < z:
    print("Smallest number is:", x)
elif y < z:
    print("Smallest number is:", y)
else:
    print("Smallest number is:", z)

```
</p>
</details> 

<details>
<summary open>Write a program to Swap two numbers. </summary>
<p>

```python
a = 5
b = 10

print("Before swapping:")
print("a =", a)
print("b =", b)

a, b = b, a

print("After swapping:")
print("a =", a)
print("b =", b)

```
</p>
</details> 

<details>
<summary open>Write a program to print Digits of a Given Number.</summary>
<p>

```python
number = 12345

print("Digits of the number:")

while number > 0:
    digit = number % 10
    print(digit)
    number = number // 10

```
</p>
</details>

<details>
<summary open>Write a program to print given number is even or odd.</summary>
<p>

```python

number = 42

if number % 2 == 0:
    print("The number is Even")
else:
    print("The number is Odd")

```
</p>
</details>

<details>
<summary open>Write a program to print given number divisible by 2 and 3.</summary>
<p>

```python

number = 18

if number % 2 == 0 and number % 3 == 0:
    print("The number is divisible by both 2 and 3")
else:
    print("The number is not divisible by both 2 and 3")

```
</p>
</details>

<details>
<summary open>Write a program to print given number divisible by 3 or 7.</summary>
<p>

```python

number = 21

if number % 3 == 0 or number % 7 == 0:
    print("The number is divisible by 3 or 7")
else:
    print("The number is not divisible by 3 or 7")

```
</p>
</details>

<details>
<summary open>Write a program to print given number divisible by 2 but not with 5.</summary>
<p>

```python
number = 14

if number % 2 == 0 and number % 5 != 0:
    print("The number is divisible by 2 but not by 5")
else:
    print("The condition is not satisfied")

```
</p>
</details>

<details>
<summary open>Write a program to print LCM - Least Common Multiple.</summary>
<p>

```python
a = 12
b = 18

if a > b:
    greater = a
else:
    greater = b

while True:
    if greater % a == 0 and greater % b == 0:
        lcm = greater
        break
    greater += 1

print("LCM of", a, "and", b, "is", lcm)

```
</p>
</details>

<details>
<summary open>Write a program to check Perfect Number.</summary>
<p>

```python
number = 28
sum_of_divisors = 0

for i in range(1, number):
    if number % i == 0:
        sum_of_divisors += i

if sum_of_divisors == number:
    print(number, "is a Perfect Number")
else:
    print(number, "is not a Perfect Number")

```
</p>
</details>


<details>
<summary open>Write a program for Temperature Converter.</summary>
<p>

```python

temperature_in_celsius = 25  # Example Celsius value
temperature_in_fahrenheit = 77  # Example Fahrenheit value

# Convert Celsius to Fahrenheit
fahrenheit = (temperature_in_celsius * 9/5) + 32
print(f"{temperature_in_celsius}°C is equal to {fahrenheit}°F")

# Convert Fahrenheit to Celsius
celsius = (temperature_in_fahrenheit - 32) * 5/9
print(f"{temperature_in_fahrenheit}°F is equal to {celsius:.2f}°C")



```
</p>
</details>
