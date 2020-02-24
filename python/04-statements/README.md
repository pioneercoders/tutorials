<h4>if</h4>

```python
# Program to check number is positive.
num = 10
if num > 0:
    print("Positive number")
```

<h4>if...else Statement</h4>

```python
# Program to check eligibility for voting.
user_age = 25

if user_age >= 18:
    print("user is eligible for voting")
else:
    print("user is not eligible for voting")
```

<h4>if...elif...else</h4>

```python
# Program to dispay grade of student.
marks = 100

if marks >= 80 and marks <=100:
    print("Destination")
elif marks 60>= 80 and marks <80:
    print("First calss")
elif marks 60>= 35 and marks <60:
    print("Second class")
else:
    print("Fail")
```
<h4>Nested if statements</h4>

```python
# In this program, we input a number
# check if the number is positive or
# negative or zero and display
# an appropriate message
# This time we use nested if
num = float(input("Enter a number: "))
if num >= 0:
    if num == 0:
        print("Zero")
    else:
        print("Positive number")
else:
    print("Negative number")
```
