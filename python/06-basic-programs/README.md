<details>
    <summary>Write a program to check given number is prime or not.</summary>
    <p>

```python
# primes numbers are integers greater than one with no positive divisors besides one and itself.
# Negative numbers are excluded.
# this function is used to check given number is prime number or not.
        
def is_prime_number(number):
    if number < 1:
        print("Invalid input.")
        raise ValueError("Value must be greater than 1.")
    count = 0;
    for i in range(1, number+1):
        if number % i == 0:
            count = count + 1

    if count == 2:
       return True
    else:
        return False

# test function
def assert_prime(actual, expected):
    if actual == expected:
        print("Test passed.")
    else:
        print("Test case failed.")

if __name__ == '__main__':
    userInput = int(input('Enter a number to check: '))
    is_prime = is_prime_number(userInput)
    if is_prime:
        print(userInput, 'is a Prime Number')
    else:
        print(userInput, 'is not a Prime Number')

    assert_prime(is_prime_number(4), False)
    assert_prime(is_prime_number(5), True)
 ```

  </p>
</details>


<details>
    <summary>Write a program to print fibonacci.</summary>
    <p>

```python
# fibonacci series: 0 1 1 2 3 5 8 etc
def fibonacci_using_loop(number):
    if number == 0: return 0
    fibonacci0, fibonacci1 = 0, 1
    print(fibonacci0)
    print(fibonacci1)
    for i in range(2, number + 1):
        fibonacci1, fibonacci0 = fibonacci0 + fibonacci1, fibonacci1
        print(fibonacci1)

if __name__ == '__main__':
    userInput = int(input('Enter the number up to which you wish to calculate fibonnaci series: '))
    fibonacci_using_loop(userInput)

 ```

  </p>
</details>

<details>
    <summary>Write a program to check palindrome.</summary>
    <p>

```python
def is_palindrome(num):
    temp = num
    rev = 0
    while num > 0:
        digit = num % 10
        rev = rev * 10 + digit
        num = num // 10
    return temp == rev

def assert_equals(expected,actual):
    if expected == actual:
        print("test passed.")
    else:
        print("test failed.")

if __name__ == '__main__':
    userInput = int(input('Enter a number to check: '))
    is_prime = is_palindrome(userInput)
    if is_prime:
        print(userInput, 'is a palindrome Number')
    else:
        print(userInput, 'is not a palindrome Number')

    assert_equals(is_palindrome(121), True)
    assert_equals(is_palindrome(56), False)
    
```

 </p>
</details>

<details>
    <summary>Write a program to find second max element in list.</summary>
    <p>
```python 
    
def second_max_ele(li):
    length = len(li)
    if length <= 1:
        print("only one or zero element is present, no second max.")
        raise ValueError("list must contains two values.")
    if len(li) == 2:
        if li[0] > li[1] :
            return li[1]
        else:
            return li[0]

    first_max = li[0]
    second_max = li[1]

    for index in range(2,length):
        if first_max < li[index]:
            second_max = first_max
            first_max = li[index]
        elif (second_max < li[index]) and (li[index] != first_max):
            second_max = li[index]

    return second_max

lis = [30,50,-10,-20,11,24,32,45,90,56,70]
print(second_max_ele(lis))
    ```


</p>
</details>