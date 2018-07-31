# dinkers.io

Knowledge share site for a group of developers.

## Setting up a local development environment

### MacOS

Install command-line tools:

```bash
xcode-select --install
```

Check ruby version:

```bash
ruby -v
2.3.3
```

If ruby isn't installed, or is an older version, install [homebrew](https://brew.sh), then install/update ruby with [homebrew](https://brew.sh):

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install ruby
```

Use ruby to install the [bundlr](https://bundler.io) and [jekyll](https://jekyllrb.com) gem packages:

```bash
gem install bundler jekyll
```

Use bundlr to install the dependencies:

```bash
bundle install
```

Use bundlr to build and serve the site at [http://127.0.0.1:4000/](http://127.0.0.1:4000/):

```bash
bundle exec jekyll serve
```

## Contributing

**Create a branch for any changes and make a pull request when the changes are complete.**

### Adding a post

Create a **Markdown** file in the relevant collection folder (`_python`, `_dev-ops`, `_static-sites`, etc). 

Add the front matter to the top of the file with the relevant information:

```markdown
---
layout: post
title:  "Decorators"
description: "A special syntax to call a function with another function as an argument."
categories: intermediate
---
```

The categories attribute is optional.

### Adding a collection

Add the folder to the root directory of the site, with the name preceded by an underscore: 

```bash
_dev-ops
_python
```

In the `_config.yml` add the title, description, and output under the collections header:

```yaml
collections:

  python:
    output: true
    description: Everything you need to be useful with the Python programming language.
```

<hr>

Special thanks to [Chester How](https://chester.how) for providing the [Tale theme](https://github.com/chesterhow/tale) that this site is based on.