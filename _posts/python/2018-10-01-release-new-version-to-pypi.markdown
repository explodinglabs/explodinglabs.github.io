---
layout: post
category: python
date: 2018-10-01
title: "Release a version to PyPI"
permalink: /python/release-to-pypi
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

This are the steps I take when releasing a version of my Python package to
PyPI.

Run some checks/cleaning. If any fail, start again.
_Recommend puttting these into pre-commit hooks._
```sh
pylint --disable=all --enable=unused-import **/*.py
mypy --disallow-untyped-defs --strict-optional package
isort -rc package
black **/*.py
```
Run tests.
```sh
pytest
rm -r .tox
tox  # Continue below while this is running
```

Update version in setup.py  
Update supported Python versions in setup.py  
Update CHANGELOG.md  
Update documentation.  

Commit:
```sh
git commit
git push
git tag (version)
git push --tags
```

Create the sdist and upload it:
```
rm -r dist
pip install -U pip
pip install -U setuptools twine
python setup.py sdist
twine check dist/*
twine upload dist/*
```

Update coverage badge:
```sh
pytest --cov-report term-missing --cov package tests
coveralls  # requires coveralls and pyyaml installed
```

Build readthedocs if there's been changes.  
Update related blog posts.  
