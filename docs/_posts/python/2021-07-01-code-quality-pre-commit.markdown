---
layout: post
category: python
title: How to use Black, Pylint and Mypy in Pre-commit?
permalink: /python/pre-commit
redirect_from:
    - /black
    - /mypy
    - /pylint
    - /checks
    - /python/checks
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

<div id="intro">
Python's not the strictest language, so to have any confidence in your code you
need to hit it with a barrage of checks to ensure it meets at least some level
of quality.
</div>

I use the following code quality checks:

- *Black* to ensure code is formatted,
- *Pylint* to disallow unused imports, and
- *Mypy* for type checking.

These pre-commit hooks will check your code when you try to commit, catching problems before they
reach your repository.

## How to install the Pre-commit hooks

Install [Pre-commit](https://pre-commit.com) and add the following `.pre-commit-config.yaml` file to the root of your
repository.

```yaml
fail_fast: true

repos:
  - repo: https://github.com/ambv/black
    rev: 22.3.0
    hooks:
      - id: black
        args: [--diff, --check]

  - repo: https://github.com/pre-commit/mirrors-pylint
    rev: v3.0.0a3
    hooks:
      - id: pylint
        args: [--disable=all, --enable=unused-import]

  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v0.902
    hooks:
      - id: mypy
        exclude: ^tests/
        args: [--strict]
```

Install them as git hooks:
```sh
pre-commit install
```

## Notes on Black

- Choose a specific Black version and be consistent with it.
  The formatting can change between versions, so what's considered
  "formatted" in one version may not be in another. _As of 2022 Black has a [Stability Policy](https://black.readthedocs.io/en/stable/the_black_code_style/index.html) which states the formatting won't change in a calendar year._
- If you have an existing project with unformatted code, format the entire
  codebase all at once. _Don't do it gradually._

Recommended: [How to use Black, Pylint and Mypy in Github Actions?](/python/github-actions)
