<details>
    <summary>Write a function check given number is prime or not.</summary>
    <p>

    ```python
        # primes numbers are integers greater than one with no positive divisors besides one and itself.
# Negative numbers are excluded.
# this function is used to check given number is prime number or not.
def is_prime_number(number):
        if number < 1:
            print("Invalid input.")
            return False
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