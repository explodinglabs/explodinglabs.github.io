<img style="margin: 0 auto;" src="https://github.com/explodinglabs/composed.blog/blob/main/docs/assets/logo.png?raw=true" />

See [Install Jekyll on a Mac](https://composed.blog/install-jekyll-on-mac).

To bring up Jekyll locally:
```sh
(cd docs && bundle exec jekyll serve --livereload)
```

To remove a post, add the following to the its meta section:
```
sitemap: false
```
This removes the post from the sitemap, and also the post listing because we
have a condition checking for that.
