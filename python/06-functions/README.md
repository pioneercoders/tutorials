
```python
>>> def print_message():
...     print(message)
...
>>> message = "Hello World!"
>>> print_message()
Hello World!
>>>
```

Again, it works. How about setting a variable in the function?

```python
>>> def get_username():
...     username = input("Username: ")
...
>>> get_username()
Username: me
>>> username
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'username' is not defined
>>>
```
## Locals and globals

So far we have used nothing but **global variables**. They are called
globals because the same variables are available anywhere in our
program, even in functions.

```python
>>> a = 1
>>> b = "hi"
>>> c = "hello"
>>> def print_abc():
...     print(a, b, c)
...
>>> print_abc()
1 hi hello
>>>
```

But there are also **local variables**. They exist only **inside**
functions, and they are deleted when the function exits.

```python
>>> def thingy():
...     d = "hello again, i'm a local variable"
...     print('inside thingy:', d)
...
>>> thingy()
inside thingy: hello again, i'm a local variable
>>> d
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'd' is not defined
>>>
```

## Input

**Note:** This section has nothing to do with the `input` function that
is used like `word = input("enter something: ")`.

So far our functions seem to be really isolated from the rest of our
code, and it sucks! But they really are not as isolated as you might
think they are.

Let's think about what the print function does. It takes an argument
and prints it. Maybe a custom function could also take an argument?

```python
>>> def print_twice(message):
...     print(message)
...     print(message)
...
>>>
```

Here `message` is an argument. When we call the function we'll get a
local variable called message that will point to whatever we passed
to `print_twice`.

