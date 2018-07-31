---
layout: post
title:  "Generators"
description: "An iterator that provides values one at a time, rather than all at once."
categories: intermediate
---

A generator object is an iterator that provides values one at a time, rather than all at once.

The benefit of this is more obvious when compared to a list.

```python
def load_pages(urls):

	html_pages = []

	for url in urls:
		html_page = requests.get(url)
		html_pages.append(html_page)

	return html_pages

```

This version of the `load_pages()` function requires all of the requests to be made, and all of the html pages to have been loaded, before anything can be done with the pages. If only the first page is required, the application must still wait until all of the pages have been downloaded before it can continue.

```python
>>> pages = load_pages(urls)
>>> inspect_page(pages[0])
```

A more useful version of this function would be one that returns the values one at a time.

```python
def load_pages_generator(urls):

	for url in urls:
		html_page = requests.get(url)
		yield html_page
```
Now the pages can be loaded and interacted with one at a time.

```python
>>> pages = load_pages_generator(urls)

>>> first_page = next(pages)
>>> inspect_page(first_page)
```

A more practical example of use would be checking the first page to check that the data is valid before committing the time and resources required to save all the pages.

```python
>>> pages = load_pages_generator(urls)

>>> first_page = next(pages)
>>> if is_valid(first_page):
... 	save_pages(first_page, pages)
```
