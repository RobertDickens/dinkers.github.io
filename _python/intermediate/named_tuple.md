---
layout: post
title:  "Named Tuple"
description: "A way to create a simple class that only serves to organise related values."
categories: intermediate
---

A named tuple is a way to create a simple class that only serves to organise related values.

## Declaration

The first argument passed is the name of the class to be created. The second argument is a list of the attributes the class should have, as strings. The return value of a named tuple is a class object.

```python
>>> from collections import namedtuple
>>> Point = namedtuple("Point", ["x", "y"])

>>> print(Point)
<class '__main__.Point'>
```

The usefulness of a named tuple is best shown by comparing it's concise declaration to that of a traditional class definition that both achieve the same result.

```python
class Point:

	def __init__(self, x=0, y=0):
		self.x = x
		self.y = y

	def __str__(self):
		return "({}, {})".format(self.x, self.y)
```
The `__init__()` and `__str__()` methods are created automatically by the named tuple.

## Basic use

The class created by named tuple can then be used as normal.

```python
>>> first_point = Point(1, 2)

>>> print(first_point)
Point(x=1, y=2)

>>> print(first_point.x, first_point.y)
1, 2
```

However the object instantiated from a class created by a named tuple can also be used as a tuple.

```python
>>> first_point[0], first_point[1]
(1, 2)

>>> x, y = first_point
>>> print(x, y)
(1, 2)
```

## Advanced use

The complexity of a class created with a named tuple may grow in the future. This complexity might require the addition of methods and additional attributes. In this case, a new more complicated class can build on the original by inheriting from it.

```python
class ComplexPoint(Point):
	...
```
