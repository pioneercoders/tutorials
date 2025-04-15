<details open>
<summary>Write a program to find Simple Interst.</summary>
<p>

```python
# Simple Interest Formula: (P × R × T) / 100

# Assigning values directly
principal = 1000      # Principal amount in rupees
rate = 5              # Rate of interest per year
time = 2              # Time in years

# Calculating simple interest
simple_interest = (principal * rate * time) / 100

# Displaying the result
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
# Compound Interest Calculator

principal = 5000        # Principal amount (P)
rate = 5                # Annual interest rate in percent
time = 3                # Time in years (T)
n = 4                   # Number of times interest is compounded per year (n)

# Convert rate to decimal
rate = rate / 100

# Calculate amount
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
<summary open> Write a program to find area of circle.</summary>
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


