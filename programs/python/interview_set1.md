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

<details open>
<summary>write a program that can print the number of prime numbers less than N and you are given a non-negative integer N</summary>
<p>

```python


```

</p>
</details>
