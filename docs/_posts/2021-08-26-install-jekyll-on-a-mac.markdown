---
layout: post
title: How to install Jekyll on a Mac?
permalink: /install-jekyll-on-mac
---

I like Jekyll but wish I didn't have to deal with Ruby!

## Install rbenv

```sh
sudo port install rbenv ruby-build
```

Put at the end of a shell startup script (`~/.zshenv` doesn't work for me so I
put it in `~/.zshrc`).

```sh
eval "$(rbenv init -)"
```

Continuing...

```sh
rbenv install 2.7.2
rbenv global 2.7.2
gem install --user-install bundler jekyll
```

## For each site

Add a `Gemfile` with dependencies (see [mine](https://github.com/explodinglabs/composed.blog/blob/main/Gemfile)).

```sh
bundle install
```

Start Jekyll. (I install Jekyll inside a `docs` subdirectory so run this from there.)

```sh
bundle exec jekyll serve --livereload
```

## If you have problems with Ruby, try:

```sh
curl -fsSL https://raw.githubusercontent.com/rbenv/rbenv-installer/main/bin/rbenv-doctor | bash
```
