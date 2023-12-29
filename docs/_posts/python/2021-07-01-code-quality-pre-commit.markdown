---
layout: post
category: python
title: How to use Ruff, Mypy, Black and Isort in Pre-commit?
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

<div id="intro" markdown="1">
Python's not the strictest language, so to have any confidence in your code it needs
to be hit with a barrage of checks to ensure it meets some level of quality.
</div>

I use the following code quality checks:

- *Ruff* for linting
- *Mypy* for type checking
- *Black* to ensure code is formatted
- *Isort* to ensure imports are grouped and sorted

These pre-commit hooks will check your code when you try to commit, catching
problems before they reach your repository.

## Install the Pre-commit hooks

Add the following `.pre-commit-config.yaml` file to the root of your
repository.

```yaml
default_language_version:
  python: python3.7

repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.8
    hooks:
      - id: ruff
        types: [python]

  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v0.971
    hooks:
      - id: mypy
        types: [python]
        args: [--strict]

  - repo: https://github.com/ambv/black
    rev: 22.8.0
    hooks:
      - id: black
        types: [python]
        args: [--check]

  - repo: local
    hooks:
      - id: isort
        name: isort
        entry: isort
        language: system
        types: [python]
        args: [--check,--profile=black]
```

Install [Pre-commit](https://pre-commit.com) and add the git hooks:
```sh
pip install precommit
pre-commit install
```

## Notes

- Isort needs to know about your project's dependencies in order to determine which groups to put your imports in. Therefore the hook
  only works with a local installation of isort, (i.e. it's installed in your
  environment).
- To exclude certain files and directories, use the exclude option, e.g. `exclude: ^(docs/|examples/request.py)`.
- If you have an existing project with unformatted code, _format the entire
  project all at once_, in a single dedicated PR. Don't do it gradually.

See also: [How to use Ruff, Mypy, Black, Isort and Pytest in Github Actions?](/python/github-actions)
