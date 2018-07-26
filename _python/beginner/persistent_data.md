---
layout: post
title:  "Persistent data"
description: "Enabling an application to maintain it's state beyond it's life."
categories: beginner
---

Persistent data allows an application to maintain state beyond its life.

## Reading and writing to files

Before interacting with a file, it must be opened. The open function takes two parameters, the location of the file, and the intended way of interacting with it.

```python
>>> text_file = open("output.txt", "w")
```

`open()` returns a file object that provides methods for working with the file. Data can be written to the file with the `write()` method.

```python
>>> line_one = "This is the first example line.\n"
>>> text_file.write(line_one)
```

After writing to the file, it should be closed to prevent any bugs or memory leaks.

```python
>>> text_file.close()
```

## Filenames and paths

Files are organised into **directories** (folders). Every running program has a **current directory**, in which default operations run. For example, a file will be automatically created in the local directory unless otherwise specified.

The `os` module can be used to work with files and directories.

```python
>>> import os
>>> current_working_directory = os.getcwd()
>>> print(current_working_directory)
'/Users/Kayra'
```

The output of `getcwd()` is a path. A simple filename, like `output.txt`, is called a relative directory, because it relies on the current directory to contextualise it. In this case the full path would be `/Users/Kayra/output.txt`

`os.path` provides other functions for working with filenames and paths. `exists()` checks whether a file or directory exists.

```python
>>> print(os.path.exists("output.txt"))
True
```

`isdir()` checks if it is a directory. `isfile()` checks if it is a file.

```python
>>> print(os.path.isdir("output.txt"))
False

>>> print(os.path.isdir("/Users/Kayra"))
True

>>> print(os.path.isfile("output.txt"))
True

>>> print(os.path.isfile("/Users/Kayra"))
False
```

`listdir()` returns a list of files and directories in the provided directory.

```python
>>> print(os.listdir(current_working_directory))
["output.txt", "development", "photos", "test.py"]
```

To demonstrate these methods, a custom function `tree()` can be created to recursively traverse through all of the child directories and print their contents.

```python
def tree(base_directory):

	for directory in os.listdir(base_directory):
		path = os.path.join(base_directory, directory)

		if os.path.isfile(path):
			print(path)
		else:
			tree(path)
```

## Databases

A database is a file that is designed to store and organise data. The module `dbm` provides an interface for creating and updating database files.

```python
>>> import dbm
>>> database = dbm.open("captions", c)

>>> database["cleese.png"] = "Photo of John Cleese."

>>> database["cleese.png"]
b'Photo of John Cleese.'
```

The object provided when reading data back from the database is a **bytes object**, denoted by the preceding **b**.

Data in a database can be changed and looped through as expected. Like files, databases should be closed after use.

```python
>>> database["cleese.png"] = "Photo of John Cleese doing a silly walk."
>>> database["cleese.png"]
b'Photo of John Cleese doing a silly walk.'

>>> for key in database:
... 	print(key, database[key])

>>> database.close()
```

## Pipes

Pipes can be used to run commands in the operating system using Python.

The **pipe object** represents a running program, and can be used with the `os.popen()` method. It can be used similarly to a file, reading the output one line at a time with `read()` and the final status with `close()` (which is usually nothing for the execution of a successful action).

```python
>>> import os
>>> file_name = "book.txt"
>>> checksum_command = "md5sum"
>>> full_command = file_name + " " + checksum_command

>>> pipe_object = os.popen(full_command)

>>> result = pipe_object.read()
>>> final_status = pipe_object.close()

>>> print(result)
1e0033f0ed0656636de0d75144ba32e0 book.txt

>>> print(final_status)
None
```

## Pickling

A drawback of `dbm` is that the keys and values have to be strings or bytes. The `pickle` module translates almost any type of object into a string suitable for storage in a database, and translates strings back into objects.


`pickle.dumps` takes an object as a parameter, and returns a byte string representation. This byte string representation can be given back to `pickle.loads` to recreate the object.

```python
>>> import pickle
>>> list_of_numbers = [1, 2, 3]
>>> list_of_numbers_data = pickle.dumps(list_of_numbers)

>>> print(list_of_numbers_data)
b'\x80\x03]q\x00(K\x01K\x02K\x03e'

>>> new_list_of_numbers = pickle.loads(list_of_numbers_data)
>>> print(new_list_of_numbers)
[1, 2, 3]

>>> list_of_numbers == new_list_of_numbers
True
>>> list_of_numbers is new_list_of_numbers
False
```
