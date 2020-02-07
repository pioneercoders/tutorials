# If, else and elif

## Using if statements

Now we know what True and False are.

```python
>>> 1 == 1
True
>>> 1 == 2
False
>>>
>>> its_raining = True
>>> its_raining
True
>>>
```

But what if we want to execute different code depending on something?
That's when `if` comes in.

```python
>>> its_raining = True
>>> if its_raining:
...     print("It's raining!")
...
It's raining!
>>> its_raining = False
>>> if its_raining:
...     print("It's raining!")        # nothing happens
...
>>>
```

## Using else

What if we want to print a different message if it's not raining? We
could do something like this:

```python
its_raining = True                  # you can change this to False
its_not_raining = not its_raining   # False if its_raining, True otherwise

if its_raining:
    print("It's raining!")
if its_not_raining:
    print("It's not raining.")
```