---
layout: post
title:  "Sets"
description: "An unordered sequence of unique and immutable objects."
categories: beginner
---

A set is an unordered sequence of unique and immutable objects.

Duplicates are removed on definition, and will not be added.

```python
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
>>> print(basket)
{'orange', 'banana', 'pear', 'apple'}

>>> basket.add('apple')
>>> print(basket)
{'orange', 'banana', 'pear', 'apple'}
```

## Decleration

An empty set can only be declared with `set()`, as curly braces will create a dictionary.

```python
>>> correct_set = set()
>>> print(type(correct_set))
<class 'set'>

>>> incorrect_set = {}
>>> print(type(incorrect_set))
<class 'dict'>
```

## Basic use

Basic uses include membership testing and eliminating duplicate entries.

```python
>>> basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}

>>> 'orange' in basket
True
>>> 'crabgrass' in basket
False
```

```python
>>> basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
>>> print(basket)
['apple', 'orange', 'apple', 'pear', 'orange', 'banana']

>>> deduplicated_basket = list(set(basket))
>>> print(deduplicated_basket)
['pear', 'orange', 'banana', 'apple']
```

## Advanced use

Set objects also support mathematical operations like union, intersection, difference, and symmetric difference.

```python
>>> a = set('abracadabra')
>>> b = set('alacazam')
```

The `intersection()` and `&` methods returns a new set with elements that are common to all sets.

```python
# letters in both a and b
>>> print(a.intersection(b))
{'a', 'c'}

>>> print(a & b)
{'a', 'c'}
```


The `union()` and `|` methods returns a new set with distinct elements from all the sets.

```python
# letters in a or b or both
>>> print(a.union(b))
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}

>>> print(a | b)
{'a', 'c', 'r', 'd', 'b', 'm', 'z', 'l'}
```


The `difference()` and `-` methods returns the set difference of two sets.

```python
# letters in a but not in b
>>> print(a.difference(b))
{'r', 'd', 'b'}

>>> print(a - b)
{'r', 'd', 'b'}
```

The `symmetric_difference()` and `^` returns a new set which is the symmetric difference of two sets.

```python
# letters in a or b but not both
>>> print(a.symmetric_difference(b))
{'r', 'd', 'b', 'm', 'z', 'l'}

>>> print(a ^ b)
{'r', 'd', 'b', 'm', 'z', 'l'}
```
