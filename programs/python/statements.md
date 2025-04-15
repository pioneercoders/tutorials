<details open>
<summary>Write a program to print Hello World.</summary>
<p>

```python
    print("Hello World!");
```

</p>
</details>

<details>
<summary open>Write a program to find Simple Interst.</summary>
<p>

```python
def calculate_simple_interest(principal, rate, time):
    simple_interest = (principal * rate * time) / 100
    return simple_interest

p = float(input("Enter the Principal amount: "))
r = float(input("Enter the Rate of interest (%): "))
t = float(input("Enter the Time (in years): "))

si = calculate_simple_interest(p, r, t)

print(f"Simple Interest = {si}")

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
