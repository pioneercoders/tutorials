<h4>What is dictionary? </h4>
<p>A dictionary is like a list, but more general. In a list, the index positions have to be integers; in a dictionary, the indices can be (almost) any type.</p>

<p>You can think of a dictionary as a mapping between a set of indices (which are called keys) and a set of values. Each key maps to a value. The association of a key and a value is called a key-value pair or sometimes an item.</p>

```python
eng2sp = {'one': 'uno', 'two': 'dos', 'three': 'tres'}
print(eng2sp)
```

<p>The function dict creates a new dictionary with no items. Because dict is the name of a built-in function, you should avoid using it as a variable name.</p>

```python
eng2sp = dict()
print(eng2sp)
eng2sp['one'] = 'uno'
print(eng2sp)
```
