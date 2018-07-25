---
layout: post
title:  "Context Managers"
description: "A context manager is a way of handling the set up and tear down required when using a persistent data store."
category: python
---

A context manager is a way of handling the set up and tear down required when using a persistent data store.

A common use is to open a file, manipulate it, then close it:

```python
with open("file.txt", "w") as file:
	file.write("Hello world.")
```

## Class based context manager

Context managers are often used with sqlite databases.

```python
from sqlite3 import connect

with connect("test.db") as connection:

	cursor = connection.cursor()

	cursor.execute("create table points(x int, y int)")

	cursor.execute("insert into points (x, y) values (1, 1)")
	cursor.execute("insert into points (x, y) values (1, 2)")
	cursor.execute("insert into points (x, y) values (2, 1)")

	for row in cursor.execute("select x, y from points")
		print(row)

	for row in cursor.execute("select sum(x * y) from points"):
		print(row)

	cursor.execute("drop table points")
```

While a context manager is already being used for the connection, another would be useful for the creation and dropping of the table in the example.

A class could be created to use the data model methods to provide a custom context manager object.

```python
class temptable:

	def __init__(self, cursor):
		self.cursor = cursor

	def __enter__(self):
		self.cursor.execute("create table points(x int, y int)")

	def __exit__(self, *args):
		self.cursor.execute("drop table points")
```

The original database code can then implement it.

```python
from sqlite3 import connect

with connect("test.db") as connection:

	cursor = connection.cursor()

	with temptable(cursor):
		cursor.execute("insert into points (x, y) values (1, 1)")
		cursor.execute("insert into points (x, y) values (1, 2)")
		cursor.execute("insert into points (x, y) values (2, 1)")

		for row in cursor.execute("select x, y from points")
			print(row)

		for row in cursor.execute("select sum(x * y) from points"):
			print(row)
```

## Generator based context manager

Because the `__enter()__` must be called before the `__exit()__`, it would be appropriate to use sequencing to enforce this.

```python
def temptable(cursor):
	cursor.execute("create table points(x int, y int)")
	yield
	cursor.execute("drop table points")
```
The original `temptable` class needs to be changed to implement this.

 ```python
 class contextmanager:

 	def __init__(self, cursor):
		self.cursor = cursor

	def __enter__(self):
		self.generator = temptable(self.cursor)
		next(self.generator)

	def __exit__(self, *args):
		next(self.generator, None)
 ```

This `contextmanager` class can then be refactored to be more general. The `__call__()` method allows arguments to be passed through to the generator.

 ```python
 class contextmanager:

 	def __init__(self, generator):
		self.generator = generator

	def __call__(self, *args, **kwargs):
		self.args, self.kwargs = args, kwargs
		return self

	def __enter__(self):
		self.generator_instance = self.generator(*self.args, **self.kwargs)
		next(self.generator_instance)

	def __exit__(self, *args):
		next(self.generator_instance, None)
 ```

The `temptable()` generator can then be wrapped with the context manager class:

```python
temptable = contextmanager(temptable)
```
Or more Pythonically:

```python
@contextmanager
def temptable(cursor):
	cursor.execute("create table points(x int, y int)")
	yield
	cursor.execute("drop table points")
```

## Contextlib

A more robust version of the context manager has already been written, and is part of the `contextlib` library.

```python
from contextlib import contextmanager
```

The only change that needs to be made to the generator to implement this decorator, is to add a `try/finally` statement.

```python
@contextmanager
def temptable(cursor):

	cursor.execute("create table points(x int, y int)")
	try:
		yield
	finally:
		cursor.execute("drop table points")
```

The pseudocode template for implementing this decorator would be as follows:

```python
@contextmanager
def context_manager_name(argument):

	set_up_code()
	try:
		yield
	finally:
		tear_down_code()
```
