<details open>
<summary>Write a program to print Arithmetic Operators </summary>
<p>
  
```python
  
# Addition (+)
    	num1 = 10
    	num2 = 5
    	sum_result = num1 + num2
    	print("Sum:", sum_result)
    
# Subtraction (-)
    	num3 = 8
    	num4 = 3
    	difference = num3 - num4
    	print("Difference:", difference)
    
# Multiplication (*)
    	num5 = 6
    	num6 = 4
    	product = num5 * num6
    	print("Product:", product)
    
# Division (/)
    	num7 = 20
    	num8 = 4
    	quotient = num7 / num8
    	print("Quotient:", quotient)
    
# Modulus (%)
    	num9 = 15
    	num10 = 7
    	remainder = num9 % num10
    	print("Remainder:", remainder)
    
# Exponentiation (**)
	base = 2
  	exponent = 3
    	result = base ** exponent
    	print("Result:", result) 
        
```
</p>
</details>

<details open>
<summary>Write a program to print Relational Operators </summary>
<p>
  
```python

# Define two variables
        x = 10
        y = 5
        
# Check if x is equal to y
        is_equal = x == y
        print(f"{x} == {y}: {is_equal}")  # Output: 10 == 5: False
        
# Check if x is not equal to y
        is_not_equal = x != y
        print(f"{x} != {y}: {is_not_equal}")  # Output: 10 != 5: True
        
# Check if x is greater than y
        is_greater = x > y
        print(f"{x} > {y}: {is_greater}")  # Output: 10 > 5: True
        
# Check if x is less than y
        is_less = x < y
        print(f"{x} < {y}: {is_less}")  # Output: 10 < 5: False
        
# Check if x is greater than or equal to y
        is_greater_equal = x >= y
        print(f"{x} >= {y}: {is_greater_equal}")  # Output: 10 >= 5: True
        
  # Check if x is less than or equal to y
        is_less_equal = x <= y
        print(f"{x} <= {y}: {is_less_equal}")  # Output: 10 <= 5: False

        
```
</p>
</details>

<details open>
<summary>Write a program to print Logiacal Operators </summary>
<p>
  
```python

# Logical AND Operator (and)
		# Returns True if both operands are True

		x = True
		y = False

		result = x and y
		print(f"{x} and {y} = {result}")  # Output: True and False = False

# Logical OR Operator (or)
		# Returns True if at least one operand is True

		result = x or y
		print(f"{x} or {y} = {result}")  # Output: True or False = True

# Logical NOT Operator (not)
		# Returns the opposite of the operands value

		result = not x
		print(f"not {x} = {result}")  # Output: not True = False

        
```
</p>
</details>

<details open>
<summary>Write a program to print Bitwise Operators </summary>
<p>
  
```python

# Bitwise AND (&)
		a = 5  # 101 in binary
		b = 3  # 011 in binary
		result_and = a & b  # 001 in binary
		print(result_and)  # Output: 1

# Bitwise OR (|)
		result_or = a | b  # 111 in binary
		print(result_or)  # Output: 7

# Bitwise XOR (^)
		result_xor = a ^ b  # 110 in binary
		print(result_xor)  # Output: 6

# Bitwise NOT (~)
		result_not_a = ~a  # -6 
		print(result_not_a)

# Left Shift (<<)
		left_shifted = a << 2  # 10100 in binary, which is 20 in decimal
		print(left_shifted)

# Right Shift (>>)
		right_shifted = a >> 1  # 10 in binary, which is 2 in decimal
		print(right_shifted)
    
```
</p>
</details>

<details open>
<summary>Write a program to print Assignment Operators </summary>
<p>
  
```python

 "Note: a += 10. Here += is an assignment operator, and the result is stored in variable a. This is same as a = a + 10."

	x = 10
	x += 5
	print(x)  # Output: 15

	x -= 3
	print(x)  # Output: 12

	x *= 2
	print(x)  # Output: 24

	x /= 3
	print(x)  # Output: 8.0

	x //= 2
	print(x)  # Output: 4.0

	x **= 3
	print(x)  # Output: 64.0

	x %= 5
	print(x)  # Output: 4.0

	x &= 7
	print(x)  # Output: 4

	x |= 8
	print(x)  # Output: 12

	x ^= 6
	print(x)  # Output: 10
    
```
</p>
</details>

<details open>
<summary>Write a program to print Ternary Operators </summary>
<p>
  
```python

	x = 10
	y = 20
	result = "x is greater" if x > y else "y is greater"
	print(result)
    
```
</p>
</details>

<details open>
<summary>Write a program to print Ternary Operators </summary>
<p>
  
```python

# Create two variables
		x = [1, 2, 3]
		y = x  # y references the same object as x

# Check if x and y refer to the same object
		if x is y:
			print("x and y refer to the same object")
		else:
			print("x and y do not refer to the same object")

# Create a new list with the same values as x
		z = [1, 2, 3]

# Check if x and z refer to the same object
		if x is z:
			print("x and z refer to the same object")
		else:
			print("x and z do not refer to the same object")

# Check if x and z do not refer to the same object
		if x is not z:
			print("x and z do not refer to the same object")
		else:
			print("x and z refer to the same object")
    
```
</p>
</details>


		


