---
layout: post
title:  "Algorithms"
description: "An algorithm is a mechanical process for solving a category of problems."
categories: beginner
---

An algorithm is a mechanical process for solving a category of problems.

An example of this would be to translate a mathematical formula to Python code (which would then be labelled as an algorithm). The computer could then run this algorithm automatically any time it is needed with varying input values.

Newton's method of finding the square root of a number is as follows:

``` python
y = (x + a/x) / 2
```

Where `a` is the number to find the square root of, `x` is the estimate of what the square root is, and `y` is the closer estimate of what the square root of `a` is.

This formula is designed to be used repeatedly until the difference between the `x` input value and `y` output value is negligible.

Writing Python code to solve this with a `while` loop would look as follows:

	def square_root(number_to_root, estimated_root):

		better_estimate = (estimated_root + number_to_root/estimated_root) / 2
		if abs(better_estimate - estimated_root) < 0.0000001:
			return better_estimate

		estimated_root = better_estimate

Comparing this to the mathematical formula:

	y = better_estimate
	x = estimated_root
	a = number_to_root
