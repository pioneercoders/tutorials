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
def calculate_compound_interest(principal, rate, time):
    amount = principal * (1 + rate / 100) ** time
    compound_interest = amount - principal
    return compound_interest

# Taking user input
p = float(input("Enter the Principal amount: "))
r = float(input("Enter the Rate of interest (%): "))
t = float(input("Enter the Time (in years): "))

# Calculating compound interest
ci = calculate_compound_interest(p, r, t)

# Display result
print(f"Compound Interest = {ci:.2f}")

```
</p>
</details> 
