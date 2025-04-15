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
