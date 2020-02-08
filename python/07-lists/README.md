<h4>Tuples </h4>
Tuples are Immutable Sequences

```python
# Create a tuple "cardinal_numbers" with "first", "second" and "third"
cardinal_numbers = ("first", "second", "third")

# Display the second object in the tuple
print(cardinal_numbers[1])

```

<h4>Lists</h4>

```python

# Exercise 1
# Create a list named food with two elements "rice" and "beans".
food = ["rice", "beans"]


# Exercise 2
# Append the string "broccolo" to the food list using .append()
food.append("brocolli")

# Exercise 3
# Add the strings "bread" and "pizza" to food using .extend()
food.extend(["bread", "pizza"])

# Exercise 4
# Print the first two items in food using slicing notation
print(food[:2])

# NOTE: The following is also acceptable
print(food[0:2])

# Exercise 5
# Print the last item in food using index notation
print(food[-1])

# Exercise 6
# Create a list called breakfast from the string "eggs, fruit, orange juice"
breakfast = "eggs, fruit, orange juice".split(", ")

# Exercise 7
# Verify that breakfast has three items using len()
print(len(breakfast) == 3)

# Exercise 8
# Create a new list called `lengths` using a list
# comprehension that contains the lengths of each
# string in the `breakfast` list.
lengths = [len(item) for item in breakfast]
print(lengths)
```

```python
items = ["Mic", "Phone", 323.12, 3123.123, "Justin", "Bag", "Cliff Bars", 134]
str_items = []
num_items = []
for i in items:
    if isinstance(i, float) or isinstance(i, int):
        num_items.append(i)
    elif isinstance(i, str):
        str_items.append(i)
    else:
        pass

print(str_items)
print(num_items)
```

```python

items = ["Microphone",  "Phone", 5502.22, "Camera", 312.33, "Cliff Bars", 423.00, "Climbing Shoes", 132, "Laptop", "Rope"]
str_items = []
int_items = []
# same list

# a-z 
str_items.sort(key=str.lower)

# z-a
str_items.sort(key=str.lower, reverse=True)


# Smallest - Largest
int_items.sort()

# Largest - Smallest
int_items.sort(reverse = True)

#To not modify the current list, use "sorted"
new_list = sorted(str_items, reverse=True)

numbers = [13, 123, 333, 423, 2341]

total = sum(numbers)
average = total/len(numbers) #rounded
average_abs = total/(len(numbers) * 1.0)
average_abs_2 = sum(numbers)/float(len(numbers))
```




