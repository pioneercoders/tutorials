<h4> Loops </h4>

In programming, a **loop** means repeating something multiple times.

<h4>For loop</h4>
    
```python
# Program to print 5 numbers.
for num in range(5):
	print(num)
```
<details>
<summary>Program to find the sum of all numbers stored in a list</summary>
<p>

```python
# List of numbers
numbers = [6, 5, 3, 8, 4, 2, 5, 4, 11]

# variable to store the sum
sum = 0

# iterate over the list
for val in numbers:
	sum = sum+val

# Output: The sum is 48
print("The sum is", sum)

```

</p>
</details>

<h4>The range() function </h4>
The range() function is used to generate the numbers.

```python
print(range(10))
print(list(range(10)))
print(list(range(2, 8)))
print(list(range(2, 20, 3)))
```

<h4> print the integer 2 through 10 using a "for" loop </h4>

```python
for i in range(2, 11):
    print(i)
```

<h4> While loops </h4>

While loops are really similar to if statements.

```python
# print the integer 2 through 10 using a "while" loop
i = 2
while i < 11:
    print(i)
    i = i + 1
 ```
 
