---
layout: post
title:  "Dictionaries"
description: "The Python implementation of a hashmap."
categories: beginner
---

A dictionary is a mapping.

A dictionary contains a collection of indices, which are called keys, and a collection of values. Each key is associated with a single value. The association of a key and a value is called a **key-value pair**, or sometimes an **item**.

Unlike lists, dictionaries are **unordered**.

``` python
>>> english_to_spanish = {
	"one": "uno",
	"two": "dos",
	"three": "tres"
}

>>> print(english_to_spanish)
{"two": "dos", "one": "uno", "three": "tres"}
```

However, the ordering is unimportant as dictionaries aren't indexed by integer indices. Instead, the defined keys are used to look up the corresponding values.

``` python
>>> print(english_to_spanish["two"])
"dos"
```

If a key does not exist in the dictionary, a `KeyError` is returned.

``` python
>>> print(english_to_spanish["four"])
KeyError: "four"
```

The `in` conditional operator can be used to see if a **key** is in the dictionary, but not the **value**.

``` python
>>> "one" in english_to_spanish
True

>>> "uno" in english_to_spanish
False
```

The `in` conditional operator can be used with the `values()` method, which returns a [dictionary view object](https://docs.python.org/3.0/library/stdtypes.html#dictionary-view-objects) making a list of values accessible.

``` python
>>> "uno" in english_to_spanish.values()
True
```

### Methods

``` python
>>> english_to_spanish = {
	"one": "uno",
	"two": "dos",
	"three": "tres"
}
```

`get` returns a value for a provided key. If the key is not in the dict, the method will either return `None` or a specified value.

``` python
>>> english_to_spanish.get("one")
"uno"

>>> english_to_spanish.get("four")
None

>>> english_to_spanish.get("five", False)
False
```

`setdefault` is similar to `get`, but will set the key to a value if it doesn't exist.

``` python
>>> english_to_spanish.get("four")
None

>>> english_to_spanish.setdefault("four", 4)
4
```

`clear` removes all elements of a dictionary.

``` python
>>> english_to_spanish.clear()
>>> print(english_to_spanish.clear)
{}
```

`copy` returns a copy of a dictionary.

``` python
>>> print(english_to_spanish)
{"one": "uno", "two": "dos", "three": "tres"}

>>> english_to_spanish_reference = english_to_spanish
>>> english_to_spanish_reference["one"] = 1
>>> print(english_to_spanish["one"])
1

>>> english_to_spanish_copy = english_to_spanish.copy()
>>> english_to_spanish_copy["two"] = 2
>>> print(english_to_spanish["two"])
"dos"
```

`fromkeys` creates a new dictionary with keys from a sequence and a possible default value.

``` python
>>> letters = ["a", "b", "c"]
>>> letters_dict = dict.fromkeys(letters)
>>> print(letters_dict)
{'a': None, 'b': None, 'c': None}

>>> counter_dict = dict.fromkeys(letters, 0)
>>> print(counter_dict)
{'a': 0, 'b': 0, 'c': 0}
```

`update` adds a dictionary to another.

``` python
>>> english_to_spanish_continued = {
	"four": "cuatro",
	"five": "cinco",
	"six": "seis"
}

>>> english_to_spanish.update(english_to_spanish_continued)
>>> print(english_to_spanish)
{"one": "uno", "two": "dos", "three": "tres", "four": "cuatro", "five": "cinco", "six": "seis"}
```

### Hashing

A hash is a function that takes a value (of any kind) and returns an integer. Dictionaries use these integers, called **hash values**, to store and look up key-value pairs.

When creating a key-value pair, Python hashes the key and stores it in the corresponding memory location. If the key is modified and used to search again, it would go to a different memory location and return an invalid value.

**Because of this, dictionary keys must be immutable. **


### Dictionary as collection of counters

A **histogram** is a statistical term for a collection of counters (or frequencies). A form of this would be a function that counts how many of each character occurs in a string.

This can be written elegantly in Python with a dictionary.

``` python
def histogram(string):

	counter_dict = dict()

	for character in string:

		if character not in counter_dict:
			counter_dict[character] = 1
		else:
			counter_dict[character] += 1

	return counter_dict
```

### Comprehension

A dictionary comprehension is an elegant, concise way of dynamically creating a dictionary.

``` python
>>> dictionary_example = {key: value for (key, value) in iterable}

>>> dictionary_example = {number: number**2 for number in range(5)}
>>> print(dictionary_example)
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

### Looping

To loop through all the values in a dictionary, it is easiest to use a `for` loop.

``` python
>>> english_to_spanish = {
	"one": "uno",
	"two": "dos",
	"three": "tres"
}

>>> for key in english_to_spanish:
... 	print(key, english_to_spanish[key])
one uno
three tres
two dos
```

### Reverse look up

If the key is known for a desired value in a dictionary, finding the value is a simple process called a `look up`.

``` python
urls['portfolio'] = "http://kayra.co.uk"
```

Finding a key in a dictionary based on a value is more difficult because of two problems.

1. There may be more than one key that maps to the same value (values are not unique in a dictionary)
2. There is no simple syntax to reverse look up.

Due to this, it is necessary to manually search a dictionary for the desired key.

``` python
def reverse_lookup(dictionary, value):

	for key in dictionary:
		if dictionary[key] == value:
			return key

	raise LookupError("The value does not appear in the dictionary")
```

This function will return the first key that matches the provided value, which may not always be the desired key. Also, this function is slow as it must traverse the entire dictionary; it's performance is related to the size of the dictionary.
