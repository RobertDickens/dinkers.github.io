---
layout: post
title:  "Ordered Dictionary"
description: "A dictionary data type that remembers the order it's keys were added."
categories: intermediate
---

An ordered dictionary data type retains it's key order. 

## Declaration

It is declared by passing it a list of tuples containing the desired key-value pairs.

```python
>>> standard_dictionary = {"a": 0, "b": 1, "c": 2, "d": 3}
>>> print(standard_dictionary) 
{'a': 0, 'c': 2, 'b': 1, 'd': 3}

>>> from collections import OrderedDict
>>> ordered_dictionary = OrderedDict([("a", 0), ("b", 1), ("c", 2), ("d",3)])
>>> print(ordered_dictionary)
OrderedDict([('a', 0), ('b', 1), ('c', 2), ('d', 3)])
```

It is possible to create an ordered dictionary from a standard dictionary:

```python
ordered_dictionary = OrderedDict(sorted(standard_dictionary.items()))
```

## Use

If a new entry overwrites an existing entry, the original insertion position is kept. However, deleting an entry and re-adding it will position it last.

```python
>>> from collections import OrderedDict
>>> ordered_dictionary = OrderedDict([("a", 0), ("b", 1), ("c", 2), ("d",3)])

>>> ordered_dictionary["a"] = 5
>>> print(ordered_dictionary)
OrderedDict([('a', 5), ('b', 1), ('c', 2), ('d', 3)])

>>> del ordered_dictionary["a"]
>>> ordered_dictionary["a"] = 5
>>> print(ordered_dictionary)
OrderedDict([('b', 1), ('c', 2), ('d', 3), ('a', 5)])
```

Equality tests between ordered dicts are order-sensitive, as seen by the implementation:

```python
list(ordered_dictionary_one.items()) == list(ordered_dictionary_two.items())
```

## Methods

The `popitem(last=True)` method is available from Python 3.1 and onwards. This will return a key-value pair and remove it from the ordered dictionary. The key-value pair returned will be done in LIFO order if `last` is True, and FIFO order if `last` is False.

```python
>>> ordered_dictionary = OrderedDict([("a", 0), ("b", 1), ("c", 2), ("d",3)])
>>> ordered_dictionary.popitem()
('d', 3)
>>> ordered_dictionary
OrderedDict([('a', 0), ('b', 1), ('c', 2)])

>>> ordered_dictionary.popitem(last=False)
('a', 0)
>>> ordered_dictionary
OrderedDict([('b', 1), ('c', 2)])
```

The `move_to_end(key, last=True)` method is available from Python 3.1 and onwards. This will move a key to the last position if `last` is True, and the first position if `last` is False. A `KeyError` will be raised if the key doesn't exist.

```python
>>> ordered_dictionary = OrderedDict.fromkeys('abcde')

>>> ordered_dictionary.move_to_end('b')
>>> ''.join(ordered_dictionary.keys())
'acdeb'

>>> ordered_dictionary.move_to_end('b', last=False)
>>> ''.join(ordered_dictionary.keys())
'bacde'

>>> ordered_dictionary.move_to_end('z')
Traceback (most recent call last):
  File "<stdin>", line 6, in <module>
KeyError: 'z'
```

---

**The standard `dict` data type is ordered by default in Python 3.7 and onwards.**