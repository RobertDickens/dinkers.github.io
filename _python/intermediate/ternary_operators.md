---
layout: post
title:  "Ternary Operators"
description: "One line conditional expressions."
categories: intermediate
---

Ternary operators allow a more concise definition of a conditional expression. This is a technique that can be used to make code cleaner and more easily maintained.

```python
message = "small" if word.length() < 100 else "large"

if word.length() < 100:
	message = "small"
else:
	message = "large"
```

Ternary operators can handle multiple `if else` statements:

```python
message = "small" if word.length() < 100 else "medium" if word.length() < 500 else "large"
```

---

Ternary operators can also be implemented with the use of tuples.

```python
("small", "large")[word.length() < 100]

if word.length() < 100:
	message = "small"
else:
	message = "large"
```

This is possible because of the way truthy and falsey values work in Python, with the first value in the tuple being of index 0 (evaluating to False), and the second value being of index 1 (evaluating to True).

This implementation sacrifices readability and performance. The syntax is uncommon and unintuitive, which makes it's incorrect implementation more likely. Additionally, both elements of the tuple are evaluated before the conditional expression is executed, resulting in needless computation unless the expression is True.

```python
number = 2 if condition else 1/0  # number will be 2

number = (1/0, 2)[condition]  # ZeroDivisionError will be raised
```