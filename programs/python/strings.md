<details open>
<summary>1️⃣ Write a program to count number of words in a string</summary>
<p>

```python
def count_words(text):
    words = text.split()
    return len(words)

# Example usage:
input_string = input("Enter a sentence: ")
word_count = count_words(input_string)
print(f"Number of words: {word_count}")
```

</p>
</details>

<details>
<summary>2️⃣ Write a program to remove all white spaces from a string</summary>
<p>

```python
def remove_spaces(text):
    return text.replace(" ", "")

# Example usage:
input_string = input("Enter a string: ")
result = remove_spaces(input_string)
print(f"String without spaces: {result}")
```

</p>
</details>

<details>
<summary>3️⃣ Write a program to find duplicate characters in a string</summary>
<p>

```python
def find_duplicates(text):
    char_count = {}
    duplicates = []

    for char in text:
        if char in char_count:
            char_count[char] += 1
        else:
            char_count[char] = 1

    for char, count in char_count.items():
        if count > 1:
            duplicates.append(char)

    return duplicates

# Example usage:
input_string = input("Enter a string: ")
duplicates = find_duplicates(input_string)
print(f"Duplicate characters: {', '.join(duplicates)}")
```

</p>
</details>

<details>
<summary>4️⃣ Write a program to convert string to integer and integer to string</summary>
<p>

```python
def string_to_integer(s):
    try:
        return int(s)
    except ValueError:
        return "Invalid string for conversion to integer"

def integer_to_string(n):
    return str(n)

# Example usage:
string_value = input("Enter a string to convert to integer: ")
integer_value = string_to_integer(string_value)
print(f"String to integer: {integer_value}")

integer_input = int(input("Enter an integer to convert to string: "))
string_result = integer_to_string(integer_input)
print(f"Integer to string: {string_result}")
```

</p>
</details>

<details>
<summary>5️⃣ Write a program to print first non-repeated character from a string</summary>
<p>

```python
def first_non_repeated_char(text):
    char_count = {}

    for char in text:
        if char in char_count:
            char_count[char] += 1
        else:
            char_count[char] = 1

    for char in text:
        if char_count[char] == 1:
            return char
    
    return "No non-repeated character found"

# Example usage:
input_string = input("Enter a string: ")
result = first_non_repeated_char(input_string)
print(f"First non-repeated character: {result}")
```

</p>
</details>
