---
layout: post
title:  "Iterators"
description: "Repeating code that acts until a task is complete."
categories: beginner
---

Iteration deals with repetitive tasks. There are multiple ways to implement repeating code that can act until a task is complete.

### While loops

A while loop runs a group of statements until a particular condition has been met.

The formal definition of the flow of execution of a while loop is as follows:

1. Determine whether the condition is true or false.
2. If false, exit the `while` statement and continue execution at the next statement.
3. If the condition is true, run the body and then go back to step 1.

An example of a while loop is as follows:

``` python
def countdown(number):

	while number > 0:
		print(number)
		number = number - 1

	print("Blast off!")
```

If the `while number is greater than zero` statement is still true, the code will print the number, and subtract one from it. After this, the value of number will be checked again, and if the statement is still true, the same code that prints and subtracts from number will be run. This will continue until the conditional statement evaluates to false.

It is also possible to end a while loop part way through the group of statements being run. To do this, use a `break`.

``` python
def countdown(number):

	while True:

		print(number)
		number = number - 1

		if number > 0:
			break

	print("Blast off!")
```

**Be wary of an infinate `while` loop. There must always be a way for the code inside the loop to reach it's terminating condition..**

### For loops

`For` loops traverse every element in a sequence. The loop continues until it has been through every element.

``` python
>>> for letter in "apple":
...    print(letter)
...
a
p
p
l
e
```
