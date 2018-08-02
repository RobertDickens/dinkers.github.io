---
layout: post
title:  "Slots"
description: "Setting instance attributes at runtime performantly."
categories: advanced
---

Internally, Python uses the `dict` data type to store an object's instance attributes. This allows easy definition of new attributes at runtime, but consumes a lot of memory for the convenience.

```python
class Employee(object):
	
	def __init__(self, start_date, salary):
		self.start_date = start_date
		self.salary = salary
		self.calculate_payment()
```

To increase performance, it is possible to use the `__slots__` feature. This will circumvent the use of a `dict` and only allocate space for a fixed set of attributes.

```python
class Employee(object):
	
	__slots__ = ["start_date", "salary"]
	def __init__(self, start_date, salary):
		self.start_date = start_date
		self.salary = salary
		self.calculate_payment()
```
