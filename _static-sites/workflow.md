---
layout: post
title:  "Static site workflow"
description: "Step by step instructions for creating a simple responsive static site."
---

## 1 Create the structure

	- index.html
	- pages
		- about.html
		- contact.html
		- timetable.html
	- js
		- main.js
	- styles
		- css
		- sass
			- styles.sass
	- resources
		- fonts
		- images

## 2 Write the markup

### Tools
**Bootstrap** - [Documentation](https://getbootstrap.com/docs/4.0/getting-started/introduction/)

Include links to CDN in the head of the document:

```html
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/css/bootstrap.min.css" integrity="sha384-PsH8R72JQ3SOdhVi3uxftmaW6Vc51MKb0q5P2rRUpPvrszuE4W1povHYgTpBfshb" crossorigin="anonymous">
<script src="https://code.jquery.com/jquery-3.2.1.slim.min.js" integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.3/umd/popper.min.js" integrity="sha384-vFJXuSJphROIrBnz7yo7oB41mKfc8JzQZiCq4NCceLEaO4IHwicKwpJf9c9IpFgh" crossorigin="anonymous"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/js/bootstrap.min.js" integrity="sha384-alpBpkh1PFOepccYVYDB4do5UnbKysX5WZXm3XxPqe5iKTfUKjNkCk9SaVuEZflJ" crossorigin="anonymous"></script>
```

## 3 Set up [build tools](https://wearejh.com/frontend-automation-with-grunt-sass-browsersync/)

### Include [gruntfile.js](./gruntfile.js) in the top level of the project

### Fill out [package.json](./package.json) and include in the top level of the project

### Install npm packages
	npm install

### Run the site and start the sass watcher
	grunt

## 4 Write SASS styles

* [Documentation](http://sass-lang.com/guide)
* [Mobile first](https://www.uxpin.com/studio/blog/a-hands-on-guide-to-mobile-first-design/)
* [Bootstrap](https://getbootstrap.com/docs/4.0/getting-started/introduction/)

## 5 Write js

## 6 Deploy