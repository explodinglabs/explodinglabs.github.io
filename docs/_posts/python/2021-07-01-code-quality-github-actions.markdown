---
layout: post
category: python
title: How to use Ruff, Mypy, Black, Isort and Pytest in GitHub Actions?
permalink: /python/github-actions
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

The following Github Actions workflow will check your code when a pull request
is created, catching problems before they're merged.

## How to add the Github Actions workflow

Add the following to your repository in `.github/workflows/code-quality.yml`.

```sh
name: Code Quality
on: [pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-python@v2
      with:
        python-version: "3.7"
    - run: pip install --upgrade pip
    - run: pip install "ruff<1" "mypy<2" "black<23" "isort<6" pytest
    - run: ruff check .
    - run: mypy --strict .
    - run: black --check .
    - run: isort --check --profile black .
    - run: pytest .
```

## Notes

- To exclude certain files and directories, use the exclude options to each tool, (usually `--exclude`).
- If you have an existing project with unformatted code, _format the entire
  project all at once_, in a single dedicated PR. Don't do it gradually.

See also: [How to use Ruff, Mypy, Black and Isort in Pre-commit?](/python/pre-commit)
