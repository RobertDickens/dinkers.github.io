---
layout: post
title:  "Strings"
description: "An unordered collection of character values"
categories: beginner
---

A string is a **sequence**, it is an ordered collection of character values.

```python
>>> string_example = "hello"
```

## Accessing characters

Individual characters of a string can be accessed with the bracket operator:

```python
>>> print("apple"[0])
a
>>> print("apple"[1])
p
```

Using decimal numbers will result in a type error:

```python
>>> print("apple"[1.5])
TypeError: string indices must be integers
```

However it is possible to use negative integers to access characters from the end of a string going backwards, starting at -1:

```python
>>> print("apple"[-1])
e
>>> print("apple"[-2])
l
```

## Slices

A slice is a segment of a string. This can also be accessed with the bracket operator.

```python
>>> string_slice = "apple"[0:3]
>>> print(string_slice)
app
```

Accessing a slice with the bracket notation will return all the characters between the numbers specified, including the first but excluding the last.

It is also possible to slice a string with one number and a colon.

```python
>>> string_slice = "apple"[:3]
>>> print(string_slice)
app

>>> string_slice = "apple"[2:]
>>> print(string_slice)
ple
```

* Omitting the first index starts the slice at the beginning of the string.
* Omitting the last index will retrieve all the characters until the end of the string.

Accessing a slice with two of the same index will result in an empty string slice.

Accessing a slice with no indices will result in a full string slice.

```python
>>> string_slice = "apple"[3:3]
>>> print(string_slice)
''

>>> string_slice = "apple"[:]
>>> print(string_slice)
apple
```

## Immutable

It's not possible to change an existing string. However it is possible to create a new string that is a variation of the original.

```python
>>> greeting = "Hello world"
>>> new_greeting = "J" + greeting[1:]
>>> print(new_greeting)
Jello world

>>> print(greeting)
Hello world
```

The original string remains unchanged.

## Methods

There are a variety of useful methods that can be used to manipulate strings.

`string.upper()` can be used to convert all the characters in a string to uppercase.

```python
>>> word = "apple"
>>> upper_case_word = word.upper()
>>> print(upper_case_word)
APPLE
```

`string.find()` can be used to find the index of a character or substring in a string. The return of a -1 value means the character or substring could not be found in the string.

```python
>>> word = "apple"

>>> character_index = word.find("l")
>>> print(character_index)
3

>>> substring_index = word.find("pl")
>>> print(substring_index)
2

>>> non_existant_character_index = word.find("z")
>>> print(non_existant_character_index)
-1
```

