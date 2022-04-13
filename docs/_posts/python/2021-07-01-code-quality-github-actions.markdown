---
layout: post
category: python
title: How to use Black, Pylint and Mypy in GitHub Actions?
permalink: /python/github-actions
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

<div id="intro" markdown="1">
Python's not the strictest language, so to have any confidence in your code you
need to hit it with a barrage of checks to ensure it meets at least some level
of quality.
</div>

I use the following code quality checks:
- *Black* to ensure code is formatted,
- *Pylint* to disallow unused imports, and
- *Mypy* for type checking.

This Github Actions workflow will check your code when a Pull
Request is created, catching problems before they're merged.

## How to add the Github Actions workflow

Add the following to your repository in `.github/workflows/code-quality.yml`.

```sh
name: Checks
on: [pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    name: Checks
    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-python@v2
      with:
        python-version: 3.x
    - run: pip install --upgrade pip
    - run: pip install "black<23" pylint==v3.0.0a3 mypy==v0.902
    - run: black --diff --check $(git ls-files '*.py')
    - run: pylint --disable=all --enable=unused-import $(git ls-files '*.py')
    - run: mypy --strict $(git ls-files '*.py')
```

## Notes on Black

- Choose a specific Black version and be consistent with it.
  The formatting can change between versions, so what's considered
  "formatted" in one version may not be in another. _As of 2022 Black has a [Stability Policy](https://black.readthedocs.io/en/stable/the_black_code_style/index.html) which states the formatting won't change in a calendar year._
- If you have an existing project with unformatted code, format the entire
  codebase all at once. _Don't do it gradually._

See also: [How to use Black, Pylint and Mypy in Pre-commit?](/python/pre-commit)
