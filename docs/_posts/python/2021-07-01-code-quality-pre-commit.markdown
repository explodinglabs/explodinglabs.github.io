---
layout: post
category: python
title: Black, Pylint and Mypy in Pre-commit
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

Python's not the strictest language, so to have any confidence in your code you
need to hit it with a barrage of checks to ensure it meets at least some level
of quality.

The tools I use are **Black** to ensure code is formatted,
**Pylint** to disallow unused imports, and **Mypy** for type checking.

Installing these Pre-commit hooks will run these checks locally on your
development machine when you try to commit, catching problems before they
reach your repository.

## Install the Pre-commit hooks

Install [pre-commit](https://pre-commit.com).

Add the following `.pre-commit-config.yaml` file to the root of your
repository.

```yaml
fail_fast: true

repos:
  - repo: https://github.com/ambv/black
    rev: 21.6b0
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

## Notes

- It's important to choose a specific Black version and be consistent with it.
  The formatting often changes between Black versions, so what's considered
  "formatted" in one version may not be in another.
- If you have an existing project with unformatted code, _format the entire
  codebase all at once_. Don't do it gradually.

Recommended: [Add these same checks to Github Actions](/python/github-actions)
