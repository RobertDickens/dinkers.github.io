---
layout: post
title:  "Sequences"
description: "A brief overview on deciding which squence data type to use."
categories: beginner
---

**Strings** are very limited in use due to the fact that their elements must be characters. Because they are immutable, it may be more beneficial to use a list of characters for computation, then `join()` afterward.

**Lists** are more common than **tuples** because they are mutable. There are some cases in which tuples might be preferred:

1. In certain cases, like `return`ing a value, it may be syntactically simpler and more concise to use a **tuple**.
2. When using a sequence as a dictionary key, an immutable data type must be used, like a **string** or a **tuple**.
3. When passing a sequence as an argument to a function, using **tuples** reduces the potential for bugs due to aliasing.

Because **tuples** are immutable, they don't have methods like `sort()` and `reverse()`. However, the sequence agnostic `sorted()` can be used to return a new list with the same elements in sorted order. `reversed()` can also be used to take a sequence and return an iterator that traverses the list in reverse order.
