# Loops

In programming, a **loop** means repeating something multiple times.
There are different kinds of loops:

- [While loops](#while-loops) repeat something while a condition is true.
- [Until loops](#until-loops) repeat something while a condition is false.
- [For loops](#for-loops) repeat something for each element of something.

We'll talk about all of these in this tutorial.

## While loops

Now we know how if statements work.

```python
its_raining = True
if its_raining:
    print("Oh crap, it's raining!")
```

While loops are really similar to if statements.

```python
its_raining = True
while its_raining:
    print("Oh crap, it's raining!")
    # we'll jump back to the line with the word "while" from here
print("It's not raining anymore.")
```

If you're not familiar with while loops, the program's output may be a
bit surprising:

    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    Oh crap, it's raining!
    (much more raining)

Again, this program does not break your computer. It just prints the
same thing multiple times. We can interrupt it by pressing Ctrl+C.

In this example, `its_raining` was the **condition**. If something in
the while loop would have set `its_raining` to False, the loop would
have ended and the program would have printed `It's not raining anymore`.

Let's actually create a program that does just that:

```python
its_raining = True
while its_raining:
    print("It's raining!")
    answer = input("Or is it? (y=yes, n=no) ")
    if answer == 'y':
        print("Oh well...")
    elif answer == 'n':
        its_raining = False     # end the while loop
    else:
        print("Enter y or n next time.")
print("It's not raining anymore.")
```
