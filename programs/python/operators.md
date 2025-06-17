<details open>
<summary>1️⃣ Arithmetic Operators</summary>
<p>

```python
# ➕ Addition
print("10 + 5 =", 10 + 5)

# ➖ Subtraction
print("8 - 3 =", 8 - 3)

# ✖️ Multiplication
print("6 * 4 =", 6 * 4)

# ➗ Division
print("20 / 4 =", 20 / 4)

# 🧮 Modulus
print("15 % 7 =", 15 % 7)

# 🔢 Exponentiation
print("2 ** 3 =", 2 ** 3)

# // Floor Division
print("17 // 3 =", 17 // 3)
```

</p>
</details>

<details>
<summary>2️⃣ Relational (Comparison) Operators</summary>
<p>

```python
x = 10
y = 5

print("x == y:", x == y)
print("x != y:", x != y)
print("x > y:", x > y)
print("x < y:", x < y)
print("x >= y:", x >= y)
print("x <= y:", x <= y)
```

</p>
</details>

<details>
<summary>3️⃣ Logical Operators</summary>
<p>

```python
x = True
y = False

print("x and y:", x and y)
print("x or y:", x or y)
print("not x:", not x)
```

</p>
</details>

<details>
<summary>4️⃣ Bitwise Operators</summary>
<p>

```python
a = 5  # 101
b = 3  # 011

print("a & b:", a & b)
print("a | b:", a | b)
print("a ^ b:", a ^ b)
print("~a:", ~a)
print("a << 2:", a << 2)
print("a >> 1:", a >> 1)
```

</p>
</details>

<details>
<summary>5️⃣ Assignment Operators</summary>
<p>

```python
x = 10

x += 5
print("x += 5:", x)

x -= 3
print("x -= 3:", x)

x *= 2
print("x *= 2:", x)

x /= 3
print("x /= 3:", x)

x //= 2
print("x //= 2:", x)

x **= 2
print("x **= 2:", x)

x %= 5
print("x %= 5:", x)

x &= 3
print("x &= 3:", x)

x |= 2
print("x |= 2:", x)

x ^= 1
print("x ^= 1:", x)

x <<= 1
print("x <<= 1:", x)

x >>= 1
print("x >>= 1:", x)
```

</p>
</details>

<details>
<summary>6️⃣ Membership Operators</summary>
<p>

```python
my_list = [1, 2, 3, 4, 5]

print("2 in my_list:", 2 in my_list)
print("10 in my_list:", 10 in my_list)
print("10 not in my_list:", 10 not in my_list)
```

</p>
</details>

<details>
<summary>7️⃣ Identity Operators</summary>
<p>

```python
a = [1, 2, 3]
b = a
c = [1, 2, 3]

print("a is b:", a is b)
print("a is c:", a is c)
print("a is not c:", a is not c)
```

</p>
</details>

<details>
<summary>8️⃣ Ternary Operator</summary>
<p>

```python
age = 18
vote_status = "Can vote" if age >= 18 else "Cannot vote"
print(vote_status)
```

</p>
</details>

<details>
<summary>9️⃣ Operator Precedence (Reference Table)</summary>
<p>

| Precedence | Operators | Description |
|------------|-----------|-------------|
| 1 (highest) | `()` | Parentheses |
| 2 | `**` | Exponentiation |
| 3 | `+x`, `-x`, `~x` | Unary plus, minus, bitwise NOT |
| 4 | `*`, `/`, `//`, `%` | Multiplication, division, modulus |
| 5 | `+`, `-` | Addition, subtraction |
| 6 | `<<`, `>>` | Bitwise shifts |
| 7 | `&` | Bitwise AND |
| 8 | `^` | Bitwise XOR |
| 9 | `|` | Bitwise OR |
| 10 | `==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `is not`, `in`, `not in` | Comparisons |
| 11 | `not` | Logical NOT |
| 12 | `and` | Logical AND |
| 13 | `or` | Logical OR |
| 14 (lowest) | `=`, `+=`, `-=`, etc. | Assignment |
```

</p>
</details>
