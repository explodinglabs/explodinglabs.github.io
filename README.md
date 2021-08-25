<img style="margin: 0 auto;" src="https://github.com/explodinglabs/explodinglabs.github.io/blob/master/assets/composed-logo-large.png?raw=true" />

## Installation

```sh
sudo port install rbenv ruby-build
rbenv init
```

Put these in your shell config file (for me, `~/.zshenv`)
```sh
if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi
export PATH="$PATH:$HOME/.gem/ruby/2.7.2/bin"
```

Continuing...
```sh
rbenv install 2.7.2
rbenv global 2.7.2
gem install --user-install bundler jekyll
bundle install
bundle exec jekyll serve --livereload
```

If you have problems with Ruby:
```sh
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash
```

## Usage

To remove a post from the list, add to post meta:
```
sitemap: false
```
This removes the post from the sitemap, and also the post listing because we
have a condition checking for that.
