---
layout: post
title:  "Lists"
description: "A sequence of values of any type."
categories: beginner
---

A list is a sequence of values of any type.

```python
>>> animals = ["ox", "wolf", "leopard"]
```

A single list can contain a variety of types:

```python
>>> example_list = ["text", 4, 3.432, ["nested_list", 43, 0]]
```

## Mutable

Values in a list can be changed individually without creating a new list.

```python
>>> animals = ["ox", "wolf", "leopard"]
>>> animals[1] = "bear"
>>> print(animals)
["ox", "bear", "leopard"]
```

## Operations

The `+` operator concatenates lists:

```python
>>> first_list = [1, 2, 3]
>>> second_list = [4, 5, 6]

>>> combined_list = first_list + second_list
>>> print(combined_list)
[1, 2, 3, 4, 5, 6]
```

The `*` operator repeats a list a given number of times:

```python
>>> [0] * 4
[0, 0, 0, 0]

>>> [1, 2, 3] * 3
[1, 2, 3, 1, 2, 3, 1, 2, 3]
```

## Slices

A slice is a segment of a list. This can also be accessed with the bracket operator.

```python
>>> letters = ["a", "b", "c", "d", "e", "f", "g"]
>>> letters_list_slice = letters[1:3]

>>> print(letters_list_slice)
["b", "c"]
```

Accessing a slice with the bracket notation will return all the elements between the numbers specified, including the first but excluding the last.

It is also possible to slice a list with one number and a colon.

```python
>>> letters_list_slice = letters[:3]
>>> print(letters_list_slice)
["a", "b", "c"]

>>> letters_list_slice = "apple"[4:]
>>> print(letters_list_slice)
["e", "f", "g"]
```

* Omitting the first index starts the slice at the beginning of the list.
* Omitting the last index will retrieve all the elements until the end of the list.

Accessing a slice with two of the same index will result in an empty list slice.

Accessing a slice with no indices will result in a full list slice.

A slice operator on the left side of an assignment can update multiple elements in the list at once.

```python
>>> letters = ["a", "b", "c", "d", "e", "f", "g"]
>>> letters[1:4] = ["x", "y", "z"]

>>> print(letters)
["a", "x", "y", "z", "e", "f", "g"]
```

## Methods

`append` adds a new element to the end of a list.

```python
>>> letters = ["a", "b", "c"]
>>> letters.append("d")

>>> print(letters)
["a", "b", "c", "d"]
```

`extend` takes a list and appends all of the elements to another list. This will leave the list being appended unmodified.

```python
>>> letters = ["a", "b", "c"]
>>> next_letters = ["d", "e", "f"]
>>> letters.extend(next_letters)

>>> print(letters)
["a", "b", "c", "d", "e", "f"]

>>> print(next_letters)
["d", "e", "f"]
```

`sort` arranges the elements of the list from low to high.

```python
>>> letters = ["g", "c", "e", "d", "b", "f", "a"]
>>> letters.sort()

>>> print(letters)
["a", "b", "c", "d", "e", "f", "g"]
```

Most list methods are void. They modify the list and return `None`

```python
>>> letters = ["g", "c", "e", "d", "b", "f", "a"]
>>> sorted_list = letters.sort()

>>> print(sorted_list)
None
```

## Map, filter and reduce

Most common list operations can be expressed as a combination of map, filter or reduce.

#### Map

A **map** is an operation that performs a function on each element in a sequence.

An example of this can be seen in creating a small function that takes a list of strings and returns a list of capitalised strings.

```python
def capitalise_strings(list_of_strings):

	list_of_capitalised_strings = []

	for string in list_of_strings:
		list_of_capitalised_strings.append(string.capitalize())

	return list_of_capitalised_strings
```

#### Filter

A **filter** is an operation that selects some of elements of a sequence and filters out the other undesired elements.

An example of this can be see in creating a small function that returns a sublist of only the uppercase strings from a list of strings.

```python
def only_uppercase_strings(list_of_strings):

	list_of_uppercase_strings = []

	for string in list_of_strings:
		if string.isupper():
			list_of_uppercase_strings(string)

	return list_of_uppercase_strings
```

#### Reduce

A **reduce** is an operation that combines a sequence of elements into a single value.

An example of this can be seen in creating a small function to sum all numbers in a list.

```python
def add_all_list_integers(list_of_integers):

	total = 0

	for integer in list_of_integers:
		total = total + integer

	return total
```

Because adding all the numbers in a list is such a common operation, Python provides a built-in function to do this:

```python
>>> list_of_numbers = [1, 2, 3]
>>> print(sum(list_of_numbers))
6
```

## Deleting elements

There are several ways to delete elements from a list.

### Pop

`pop` takes an index, modifies the list to remove the vaue at that index and returns the value that was removed. If no index is provided, it deletes and returns the last element.

```python
>>> letters = ["a", "b", "c"]
>>> letter = letters.pop(1)

>>> print(letters)
["a", "c"]

>>> print(letter)
"b"
```

### Del

If the value won't be needed after removal, `del` is more appropriate.

```python
>>> letters = ["a", "b", "c"]
>>> del letters[1]

>>> print(letters)
["a", "c"]
```

### Del slice

`del` can be combined with slicing to remove multiple elements at once.

```python
>>> letters = ["a", "b", "c", "d", "e", "f", "g"]
>>> del letters[1:4]

>>> print(letters)
["a", "e", "f", "g"]
```

### Remove

The `remove` operator can be used to remove elements by value instead of index.

```python
>>> letters = ["a", "b", "c"]
>>> letters.remove("b")

>>> print(letters)
["a", "c"]
```

**The `remove` operator will only remove a single element, even if multiple elements of the same value exist in the list**


## Strings

### Casting

Because a string is a sequence of characters and a list is a sequence of elements, a string can be converted to a list just by using the `list()` definition as a type cast.

```python
>>> name = "Rob"
>>> list_name = list(name)

>>> print(list_name)
["R", "o", "b"]
```

### Splitting

It is also possible to split a long string containing multiple words into a list of those words using the `split` method.

```python
>>> sentence = "My name is Rob"
>>> list_sentence = sentence.split()

>>> print(list_sentence)
["My", "name", "is", "Rob"]
```

The default delimiter (which is passed as a parameter to the `split` function) is a space. Meaning that the string will be split into elements whenever there is a space.

This can be changed by passing a different character as a parameter to be used as a splitting delimiter.

```python
>>> sentence = "spam-spam-spam"
>>> list_sentence = sentence.split("-")

>>> print(list_sentence)
["spam", "spam", "spam"]
```

### Joining

`join` is the inverse of split. It takes a list of strings and concatenates the string elements into one string. This method also takes a delimiter.

```python
>>> list_sentence = ["My", "name", "is", "Rob"]
>>> sentence = " ".join(list_sentence)

>>> print(sentence)
"My name is Rob"
```

## Objects and values

```python
>>> first_string = "abc"
>>> second_string = "abc"
```

When creating two strings of the same value there a two possibilities of how Python handles this internally.

1. The first and second string refer to two different objects that have the same value
2. The first and second string refer to the same value

This can be determined with the `is` conditional operator.

```python
>>> first_string is second_string
True
```

This deduction shows that Python only created one string object, and both variables refer to it.

However, when creating two lists, this is not true.

```python
>>> first_list = ["a", "b", "c"]
>>> second_list = ["a", "b", "c"]

>>> first_list is second_list
False
```

The two lists are **equivalent**, because they contain the same elements, but they are not **identical**, because they are not the same object.

The terms **object** and **value** are often used interchangeably, but it is more precise to say that an **object** has a **value**. Based on this we can say that the two lists have the same values, but are different objects.

## Aliasing

If `a` refers to an object, and `a` is assigned to `b`, then both variables refer to the same object

```python
>>> a = [1, 2, 3]
>>> b = a

>>> b is a
True
```

The association of a variable with an object is called a reference.

An object with more than one reference has more than one name, the technical term is to say that the object is **aliased**.

If the aliased object is mutable, changes made with one alias affect the other.

```python
>>> a = [1, 2, 3]
>>> b = a
>>> b[0] = 42

>>> print(a)
```