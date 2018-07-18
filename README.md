# dinkers.io

Knowledge share site for a group of developers.

## Set up local development environment

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