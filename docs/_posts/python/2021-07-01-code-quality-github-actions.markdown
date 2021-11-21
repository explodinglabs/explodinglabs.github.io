---
layout: post
category: python
title:  Use Black, Pylint and Mypy in GitHub Actions
permalink: /python/github-actions
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

**Python's not the strictest language, so to have any confidence in your code you
need to hit it with a barrage of checks to ensure it meets at least some level
of quality.**

The tools I use are *Black* to ensure code is formatted,
*Pylint* to disallow unused imports, and *Mypy* for type checking.

Adding this _Github Actions_ workflow will run a series of checks when a pull
request is created, catching problems before they're merged.

## Add the Github Actions workflow

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
    - run: pip install black==21.6b0 pylint==v3.0.0a3 mypy==v0.902
    - run: black --diff --check $(git ls-files '*.py')
    - run: pylint --disable=all --enable=unused-import $(git ls-files '*.py')
    - run: mypy --strict $(git ls-files '*.py')
```

## Notes

- It's important to choose a specific Black version and be consistent with it.
  The formatting often changes between Black versions, so what's considered
  "formatted" in one version may not be in another.
- If you have an existing project with unformatted code, _format the entire
  codebase all at once_. Don't do it gradually.

See also: [Add these same checks to Pre-commit](/python/pre-commit)
