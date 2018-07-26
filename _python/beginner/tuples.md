---
layout: post
title:  "Tuples"
description: "An immutable sequence of values"
categories: beginner
---

A tuple is an immutable sequence of values. The values can be any type, and are indexed by integers. They are similar to lists, but the important distinction is that they are immutable.

## Assignment

```python
>>> example_tuple = "a", "b", "c", "d", "e", "f", "g"
```

While not necessary, it is common to enclose tuples in parentheses.

```python
>>> example_tuple = ("a", "b", "c", "d", "e", "f", "g")
```

Defining a tuple of a single value is slightly different. The value must have a trailing comma, parentheses are not enough.

```python
>>> example_tuple = "a",
>>> print(type(example_tuple))
<class 'tuple'>

>>> incorrect_example_tuple = ("a")
>>> print(type(incorrect_example_tuple))
<class 'str'>
```


It is also possible to instantiate and empty tuple with it's keyword and no arguments.

```python
>>> example_tuple = tuple()
>>> print(example_tuple)
()
```

If a sequence is passed as an argument, the result is a tuple with the elements of the sequence.

```python
>>> example_tuple = tuple("test")
>>> print(example_tuple)
("t", "e", "s", "t")
```

Accessing tuples with indices and slicing tuples works in the same way as with lists.

```python
>>> example_tuple = ("t", "e", "s", "t")

>>>	 print(example_tuple[0])
"t"

>>> print(example_tuple[1:3])
("e", "s")
```

Trying to modify one of the elements results in an error.

```python
>>> example_tuple = ("t", "e", "s", "t")
>>> example_tuple[0] = "T"
TypeError: object doesn't support item assignment
```

However it is possible to replace one tuple with a modified version of itself.

```python
>>> example_tuple = ("t", "e", "s", "t")
>>> example_tuple = ("A",) + example_tuple[1:]

>>> print(example_tuple)
("T", "e", "s", "t")
```

## Tuple unpacking

**Tuple unpacking** can be used as an elegant solution for swapping variables.

Example of variable swapping with a traditional temporary variable:

```python
>>> temp = a
>>> a = b
>>> b = temp
```

Example of swapping variables with tuple assignment

```python
>>> a, b = b, a
```

One requirement of tuple unpacking is that both sides have the same number of values.

```python
>>> a, b = 1, 2, 3
ValueError: too many values to unpack
```

## Tuples as return values

A functional can only return one value. Tuples are the easiest way to return multiple values, a single tuple can contain multiple values thus satisfying the functions requirements to only return one value despite logically returning multiple.

An example of where this would be useful is the `divmod()` function, that takes two numbers and returns a tuple containing the quotient and the remainder.

```python
>>> quotient, remainder = divmod(7, 3)

>>> print(quotient)
2

>>> print(remainder)
1
```

A simple example of a function that returns a tuple would be as follows:

``` python
def first_and_last(sequence):
	return sequence[0], sequence[-1]
```

## Relational operators

Relational operators evaluate sequences by comparing elements in order of index, one at a time. Equal elements are skipped, and the first unequal pair is compared.

```python
>>> (0, 1, 2) <	(0, 3, 4)
True
```

After a pair has been evaluated, subsequent elements are not considered.

```python
>>> (0, 1, 2000000) < (0, 3, 4)
True
```

## Tuples and lists

`zip()` is a built-in function that takes two or more sequences and returns a list of tuples. Each tuple in the list contains one element from each sequence.

```python
>>> string_to_zip = "abc"
>>> list_to_zip = [1, 2, 3]
>>> zip_example = zip(string_to_zip, list_to_zip)

>>> for pair in zip_example:
... 	print(pair)

("a", 1)
("b", 2)
("c", 3)
```

`zip()` returns an iterator, which is an object that iterates through a sequence. To use the return of a zip like a list, it can be be cast to one.

```python
>>> print(list(zip_example))
[("a", 1), ("b", 2), ("c", 3)]
```

If the sequences are not the same length, the resulting iterator will be the length of the shortest sequence.

```python
>>> print(list(zip("Anne", "Elk")))
[("A", "E"), ("n", "l"), ("n", "k")]
```

Tuple unpacking can be used to concisely traverse a list of tuples.

```python
>>> list_of_tuples = [("a", 1), ("b", 2), ("c", 3)]
>>> for letter, number in list_of_tuples:
... 	print(letter, number)
a 1
b 2
c 3
```

In this way, zip can be combined with other tools to easily compute tasks on more than one sequence at the same time, for example comparison.

```python
def has_match(sequence_one, sequence_two):

	for element_one, element_two:
		if element_one == element_two:
			return True

	return False

```

## Tuples and dictionaries

Dictionaries have a method called `items()` that returns a sequence of tuples, each tuple containing a key-value pair.

```python
>>> example_dictionary = {
... 	"a": 1,
...		"b": 2,
... 	"c": 3
... }

>>> print(example_dictionary.items())
dict_items([("b": 2), ("c": 3), ("a": 1)])

>>> for key, value in example_dictionary.items():
... 	print(key, value)
b 2
a 1
c 3
```

In the opposite manner, a dictionary can be instantiated with a list of tuples.

```python
>>> list_of_tuples = [("a", 1), ("b", 2), ("c", 3)]
>>> dictionary_from_tuples = dict(list_of_tuples)
>>> print(dictionary_from_tuples)
{"a": 1, "c": 3, "b": 2}
```

`zip()` can also be used to combine two sequences that can be used to instantiate a dictionary.

```python
>>> example_dictionary = dict(zip("abc", range(3)))
>>> print(example_dictionary)
{"a": 0, "c": 2, "b": 1}
```

It is common to use tuples in keys as lists can't be used (mutable vs immutable).

An example of this would be in storing telephone numbers in a dictionary with first and last names as keys.

```python
directory[last_name, first_name] = phone_number
```

Then tuple unpacking can be used to traverse the dictionary.

```python
>>> for last_name, first_name in directory:
... 	print(first_name, last_name, directory[last_name, first_name])
```
