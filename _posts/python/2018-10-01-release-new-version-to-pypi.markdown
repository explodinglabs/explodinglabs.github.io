---
layout: post
category: python
title: Release a version to PyPI
permalink: /python/release-to-pypi
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

These are the steps I take when releasing a version of my Python package to
PyPI.

First run your checks/cleaning. I have a post about this [here](/checks). If
any fail, start again.

Run tests.
```sh
pytest
rm -r .tox; tox  # Continue below while this is running
```

Update version in setup.py  
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
pip install --upgrade pip setuptools twine
python setup.py sdist
twine check dist/my_package-x.x.x.tar.gz
twine upload dist/my_package-x.x.x.tar.gz
```

Update coverage badge:
```sh
pytest --cov-report term-missing --cov package tests  # requires pytest-cov
coveralls  # requires coveralls and pyyaml installed
```

Build readthedocs if there's been changes.  
Update related blog posts.  
