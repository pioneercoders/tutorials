<details open>
<summary>write a program that can print the number of prime numbers less than N and you are given a non-negative integer N</summary>
<p>

```python
   def is_prime(num):
    if num < 2:
        return False
    for i in range(2, int(num ** 0.5) + 1):
        if num % i == 0:
            return False
    return True

def count_primes(n):
    count = 0
    for i in range(n):
        if is_prime(i):
            count += 1
    return count

# Example: Input from user
N = int(input("Enter a non-negative integer: "))
print("Number of prime numbers less than", N, "is:", count_primes(N))

```

</p>
</details>

<details>
<summary>Given two binary strings a and b,Write a program to find their sum as a binary string and perform the binary addition operation on these values</summary>
<p>

```python
def add_binary(a, b):
    # Convert binary strings to integers
    num1 = int(a, 2)
    num2 = int(b, 2)
    
    # Add the integers
    total = num1 + num2
    
    # Convert the result back to binary string and remove '0b' prefix
    return bin(total)[2:]

# Example usage
a = input("Enter first binary number: ")  # e.g., 1010
b = input("Enter second binary number: ") # e.g., 1101

result = add_binary(a, b)
print(f"Binary sum of {a} and {b} is: {result}")


```

</p>
</details>

<details open>
<summary>Given two binary strings a and b,Write a program to find their sum as a binary string and perform the binary addition operation on these values</summary>
<p>

```python


```

</p>
</details>
