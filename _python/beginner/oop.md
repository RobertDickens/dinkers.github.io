---
layout: post
title:  "Object Oriented Programming"
description: "A social construct that uses programmer defined types to organise code and data."
categories: beginner
---

OOP is the use of programmer defined types to organise code and data. It is a social construct, not something inherent in computer science.

## Classes and objects

As well as Python's built-in types, it is possible to create custom types via a `class`.

An example of this would be to create a class called `Point` to represent a point in a two dimensional space (x, y). This could be represented in multiple ways in Python:

1. Store the coordinates in two variables, x and y.
2. Store the coordinates as elements in a list or tuple.
3. Create a new type to represent the points as objects.

### Defining a class

A class must first be declared with a `class` header and a name. It can then be defined with data and behaviour, for now Point will be kept simple with only documentation.

```python
>>> class Point:
... 	"""Represents a point in a 2-D space."""
... 	pass
```

### Instantiating an object

An object of the class must be instantiated before it can be used. Multiple objects can be instantiated from the same class. A class can be thought of as a blueprint, and objects thought of as buildings.

```python
>>> initial_point = Point()
>>> final_point = Point()
```

### Attributes

Attributes are named elements of an object. These can be assigned and read with dot notation.

```python
>>> initial_point.x = 3.0
>>> initial_point.y = 4.0

>>> print(initial_point.x)
3.0

>>> y_point = initial_point.y
>>> print(y_point)
4.0
```

### Properties and methods

A method is a function that belongs to a class. A property is a variable that belongs to a class. These can then be used with an instantiated object.

**Properties** need to be defined in the `__init__()` method of a class. This method is run as soon as an object is instantiated, and is where any set up functionality should go.

**Methods** need to be defined with a `self` parameter. This `self` parameter refers to the object that has been instantiated when an object is created from a class, and is what allows Python to tell apart two different objects from the same class.

It can be thought of as a surrogate for an object's name. Because the object hasn't been instantiated or given a name, and could be given any name, `self` is used.

```python
>>> class Point:
...
... 	"""Represents a point in a 2-D space."""
...
... 	def __init__(self):
... 		self.x = 2.0
... 		self.y = 2.0
...
...		def full_point(self):
...			return self.x, self.y

>>> initial_point = Point()
>>> print(initial_point.full_point)
2.0, 2.0

>>> initial_point.x = 5.0
>>> print(initial_point.full_point)
5.0, 2.0
```

## Copying

Copying an object is an alternative to aliasing. The copy module contains a function called `deepcopy()` that can duplicate an object.

The two objects will contain the same data, but not be the same object. This can be proven in this simple case by printing the values of a copied object, and using an `is` conditional operator.

```python
>>> from copy import deepcopy

>>> point_one = Point()
>>> point_one.x = 5.0
>>> point_one.y = 7.0

>>> point_two = deepcopy(point_one)

>>> print(point_two.x, point_two.y)
5.0, 7.0

>>> print(point_one is point_two)
False
```

The `==` operator will also evaluate to `False` as Python is unable to check object equivalence, only object identity.

The `copy` module also provides the `copy` method, which is a **shallow copy**, which copies an object and any references it contains, but not embedded objects.

## Encapsulation

Encapsulation is the restriction of access to methods and variables. There are three main reasons for this.

### 1 Design by contract

Data encapsulation allows the enforcement of class invariants (unchangeable variables), preconditions and postconditions.

An example would be the creation of a `Clock` class. In this case, the class invariants would be the **hours**, which could only be set between 1 and 12, **minutes** being set between 0 and 59, and **seconds** being set between 0 and 59. Making these fields private ensures that no one is able to set them to illegal values.

Making data private means code is less likely to be misused, and is thus more robust and reliable.

### 2 Human interface

The smaller an API is, the easier it is to learn, understand, and be used correctly. Marking code as private results in more gentle learning curve of an API, and improves ease of use.

### 3 Separating implementation from interface

By making internal code unavailable for use, this code can be rewritten and refactored with the confidence that nothing else will break. As long as the input and the output remain the same (interface), the implementation can be changed to improve performance or readability without the risk of breaking something else that was using it.

```python
>>> class Car:
...
... 	def __init__(self):
... 		self.__update_software()
...
...		def drive(self):
... 		print("Driving")
...
... 	def __update_software(self):
... 		print("Updating software")

>>> race_car = Car()
Updating software

>>> race_car.drive()
Driving

>>> race_car.__update_software()
AttributeError: 'Car' object has no attribute '__update_software'
```
In Python, the double underscore notation `__` is used to mark methods and properties as private.

## Inheritance

Inheritance is the derivation of one class from another, commonly described as creating a **child** class from a **parent** class. The child class inherits all data and behaviour from the parent class, and can change it as needed without effecting the parent class.

```python
>>> class Employee:
...
... 	def __init__(self):
... 		self.salary = 0
... 		self.bonus_multiplier = 0
...
... 	def calculate_bonus(self):
... 		return self.salary * self.bonus_multiplier

>>> class Cashier(Employee):
...
... 	def __init__(self):
... 		self.salary = 500
... 		self.bonus_multiplier = 2

>>> class Manager(Employee):

... 	def __init__(self):
... 		self.salary = 1000
... 		self.bonus_multiplier = 3

>>> richard = Cashier()
>>> print(richard.calculate_bonus)
1000

>>> piana = Manager()
>>> print(piana.calculate_bonus)
3000
```

Both `Cahsier` and `Manager` classes **inherited** the `calculate_bonus()` method from `Employee`. Because of this, once their `salary` and `bonus_multiplier` properties were defined, both were able to use the calculate bonus functionality separately.

## Polymorphism

Polymorphism is the definition of the same function on objects of different classes.

A simple example of this is the built-in function `len()`

```python
>>> print(len("hello"))
5

>>> print(len([1, 2, 3]))
3
```
Despite the two different data types **string** and **list** (which are created from internal Python classes), `len()` provides consistent behaviour for both (and all built-in) sequences.

The `len()` function is defined in the sequence class that both **string** and **list** inherit. In each **string** and **list**, the `len()` method is overloaded and implemented in a way relevant to the specific sequence.

Polymorphism keeps code DRY, which improves maintainability and extensibility.

## Composition

Composition is the use of object instantiation in class definitions to delegate to other classes in the place of multiple inheritance.

```python
>>> class Math1:
...
... 	def __init__(self, x, y):
... 		self.x = x
... 		self.y = y
...
... 	def add(self):
... 		return self.x + self.y
...
... 	def subtract(self):
... 		return self.x - self.y

>>> class Math2:
...
... 	def __init__(self, x, y):
... 		self.x = x
... 		self.y = y
...
... 	def multiply(self):
... 		return self.x * self.y
...
... 	def divide(self):
... 		return self.x / self.y
```
To create a new class that can use all of these methods and add more, composition can be used to instantiate `Math1` and `Math2` in the `__init__()` method of a new class.

```python
>>> class Math3:
...
... 	def __init__(self, x, y):
... 		self.x = x
... 		self.y = y
... 		self.math1 = Math1(x, y)
... 		self.math2 = Math2(x, y)
...
... 	def power(self):
... 		return self.x ** self.y
...
... 	def add(self):
... 		return self.math1.add()
...
... 	def subtract(self):
... 		return self.math1.subtract()
...
... 	def multiply(self):
... 		return self.math2.multiply()
...
... 	def divide(self):
... 		return self.math2.divide()

>>> math = Math3(8, 3)

>>> print(math.add())
11

>>> print(math.multiply())
24

>>> print(math.power())
512
```
