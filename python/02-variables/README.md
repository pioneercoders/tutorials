## Variables

Variables are easy to understand. They simply **point to values**.

```python
>>> a = 1   # create a variable called a that points to 1
>>> b = 2   # create another variable
>>> a       # get the value that the variable points to
1
>>> b
2
>>>
```

When assigning something to a variable using a `=`, the right side of
the `=` is always executed before the left side. This means that we can
do something with a variable on the right side, then assign the result
back to the same variable on the left side.

```python
>>> a = 1
>>> a = a + 1
>>> a
2
>>>
```

## Booleans

There are two Boolean values, True and False. In Python, and in many
other programming languages, `=` is assigning and `==` is comparing.
`a = 1` sets a to 1, and `a == 1` checks if a equals 1.

```python
>>> a = 1
>>> a == 1
True
>>> a = 2
>>> a == 1
False
>>>
```

## None

None is Python's "nothing" value. It behaves just like any other value,
and it's often used as a default value for different kinds of things.
Right now it might seem useless but we'll find a bunch of ways to use
None later.

None's behavior on the interactive prompt might be a bit confusing at
first:

```python
>>> thingy = None
>>> thingy
>>>
```
