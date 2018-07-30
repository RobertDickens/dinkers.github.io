---
layout: post
title:  "Counters"
description: "A dictionary subclass for counting immutable (hashable) objects."
categories: intermediate
---

A Counter is a dictionary subclass for counting immutable (hashable) objects.

It is an unordered collection where elements are stored as dictionary keys and their counts are stored as dictionary values. Counts are allowed to be any integer value including zero or negative counts.

## Declaration

A counter object can be instantiated in a variety of ways.

```python
>>> from collections import Counter

# a new, empty counter
>>> print(Counter())
>>> Counter()

# a new counter from a sequence
>>> print(Counter('gallahad'))
Counter({'a': 3, 'l': 2, 'g': 1, 'h': 1, 'd': 1})

# a new counter from a mapping
>>> print(Counter({'red': 4, 'blue': 2}))
Counter({'red': 4, 'blue': 2})

# a new counter from keyword arguments
>>> print(Counter(cats=4, dogs=8))
Counter({'dogs': 8, 'cats': 4})
```

## Basic use

Counter objects have a dictionary interface, except that they return a zero count for missing items instead of raising a `KeyError`:

```python
>>> breakfast = Counter(['eggs', 'ham'])
>>> breakfast['bacon']
0
```

Setting a count to zero does not remove an element from a counter. Use del to remove it entirely:

```python
>>> breakfast['eggs'] = 0
>>> print(breakfast)
Counter({'eggs': 0, 'ham': 0})

>>> del breakfast['eggs']
Counter({'ham': 0})
```

## Advanced use

Counter objects support three methods beyond those available for all dictionaries: `elements()`, `most_common()` and `subtract()`

The `elements()` method returns an iterator over elements repeating each as many times as it's count. Elements are returned in arbitrary order and if an element’s count is less than one, `elements()` will ignore it.

```python
>>> counter = Counter(a=4, b=2, c=0, d=-2)
>>> print(sorted(counter.elements()))
['a', 'a', 'a', 'a', 'b', 'b']
```

The `most_common()` method returns a list of a given number of most common elements and their counts from the most common to the least. If the arguement is omitted or None, most_common() returns all elements in the counter. Elements with equal counts are ordered arbitrarily.

```python
>>> print(Counter('abracadabra').most_common(3))
[('a', 5), ('r', 2), ('b', 2)]
```

The `subtract()` method subtracts elements from an iterable or from another mapping (or counter). Similar to `dict.update()`, but subtracts counts instead of replacing them. Both inputs and outputs may be zero or negative.

```python
>>> counter_one = Counter(a=4, b=2, c=0, d=-2)
>>> counter_two = Counter(a=1, b=2, c=3, d=4)

>>> counter_one.subtract(counter_two)
>>> print(counter_one)
Counter({'a': 3, 'b': 0, 'c': -3, 'd': -6})
```
