---
layout: post
title:  "Bootstrap recipes"
description: "Practical recipes for common Bootstrap use."
---

## Single column responsive

```html
<div class="container-fluid">
  <div class="row">
    <div class="col offset-sm-1 col-sm-10 offset-md-2 col-md-8 offset-lg-2 col-lg-8">
	  { content }
	</div>
  </div>
</div>
```

## Three column large screen to single column stack small screen

```html
<div class="container-fluid">
    <div class="row">

        <div class="col-12 col-sm-12 col-md-4 col-lg-4">
		  { content }
        </div>

        <div class="col-12 col-sm-12 col-md-4 col-lg-4">
		  { content }
        </div>

        <div class="col-12 col-sm-12 col-md-4 col-lg-4">
		  { content }
        </div>

    </div>
</div>
```