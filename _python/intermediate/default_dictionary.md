---
layout: post
title:  "Default Dictionary"
description: "A dictionary that automatically generates empty values for keys that don't exist."
categories: intermediate
---

A `defaultdict` is a dictionary that automatically generates empty values for keys that don't exist.

## Declaration

A `defaultdict` must be passed a **factory** when declared so that it knows what type the empty value should be when automatically creating it.

A **factory** is a function used to create new objects. The built-in functions used to create lists, sets, etc. are common examples of factories.

```python
>>> from collections import defaultdict
>>> example_defaultdict = defaultdict(list)

>>> print(example_defaultdict)
defaultdict(<class 'list'>, {})
```

Note that the argument is a `list` class object, rather than the declaration of a new list object, `list()`. The function provided doesn't get called until a non-existent key is accessed.

## Use

Trying to access a key that does not exist will create a key provided and an empty value using the type of the factory provided.

```python
>>> example_nonexistent_value = example_defaultdict['nonexistent_key']
>>> print(example_nonexistent_value)
[]
```

If the new alias representing the value of this key is changed, it is changed in the default dict also.

```python
>>> example_nonexistent_value.append("new value")
>>> print(example_defaultdict)
defaultdict(<class 'list'>, {'example_nonexistent_value.append': ['new value']})

>>> example_nonexistent_value.append("second value")
>>> print(example_defaultdict)
defaultdict(<class 'list'>, {'example_nonexistent_value.append': ['new value', 'second value']})
```
