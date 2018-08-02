---
layout: post
title:  "Mutability"
description: "What it means for a data type to be mutable."
categories: intermediate
---

Mutable things are changeable, immutable things are constant. There are important features of mutable data types that should be known.

Whenever a variable is assigned to another variable that is mutable, any changes to data are reflected by both variables. The new variable is an alias of the old one, two names for the same piece of data.

```python
foo = ['hi']
print(foo)  # ['hi']

bar = foo
bar += ['bye']

print(foo)  # ['hi', 'bye']

print(bar)  # ['hi', 'bye']
```

In Python, the default arguments for a function are evaluated when the function is defined at run time, not each time the function is called. Combined with the way mutable data types are handled, this can cause unintended functionality.

```python
def add_to(num, target=[]):
    target.append(num)
    return target

add_to(1)  # [1]

add_to(2)  # [1, 2]

add_to(3)  # [1, 2, 3]
```
To achieve the desired functionality, it is necessary to explicitly include logic that forces the default argument to be handled when the function is called.

```python
def add_to(element, target=None):
    if target is None:
        target = []
    target.append(element)
    return target

add_to(1)  # [1]

add_to(2)  # [2]

add_to(3)  # [3]
```