<h4> Loops </h4>

In programming, **loop** are used to do repeating based on condition.

<h4>For loop</h4>
    
```python
# Program to print 5 numbers.
for num in range(5):
	print(num)
```
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
 
<details>
<summary>Program to prints various patterns</summary>
<p>

```python
def pattern1(level):
    '''This function prints the following pattern:
    *
    **
    ***
    ****

    '''
    for i in range(1, level + 1):
        print()
        for j in range(i):
            print('*', end = '')

def pattern2(level):
    '''This function prints the following pattern:

    ****
    ***
    **
    *

    '''
    for i in range(level, 0, -1):
        print()
        for j in range(i):
            print('*', end = '')

def pattern3(level):
    '''This function prints the following pattern:

       *
      **
     ***
    ****

    '''
    counter = level
    for i in range(level + 1):
        print(' ' * counter + '*' * i)
        counter -= 1

def pattern4(level):
    '''This function prints the following pattern:

    ****
     ***
      **
       *

    '''
    counter = 0
    for i in range(level, 0 ,-1):
        print(' ' * counter + '*' * i)
        counter += 1

def pattern5(level):
    '''This function prints the following pattern:

      *
     ***
    *****

    '''
    # first loop for number of lines
    for i in range(level + 1):
        #second loop for spaces
        for j in range(level - i):
            print (" ",end='')
        # this loop is for printing stars
        for k in range(2 * i - 1):
            print("*", end='')
        print()


if __name__ == '__main__':
    userInput = int(input('Enter the level: '))
    pattern1(userInput)
    print()
    pattern2(userInput)
    print()
    pattern3(userInput)
    print()
    pattern4(userInput)
    print()
    pattern5(userInput)
    print()

    def pattern6(userInput):
        '''
        following is the another approach to solve pattern problems with reduced time complexity 

        for 

        *
        **
        ***
        ****
        *****
        '''

        num = int(input('Enter number for pattern'))
        pattern = '*'
        string = pattern * num
        x = 0

        for i in string:
            x = x + 1
            print(string[0:x])
```


</p>
</details>

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