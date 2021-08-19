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

In a new branch:
- Update version in setup.py.
- Update `README.md`, if any.
- Update `CHANGELOG.md` - stable releases only.
- Update documentation.

Commit, push and merge into master.

Pull master, tag the commit and push the tag.

Create the sdist and upload it:
```
pip install --upgrade pip setuptools twine
python setup.py sdist
twine check dist/my_package-x.x.x.tar.gz
twine upload dist/my_package-x.x.x.tar.gz
```

Update coverage badge:
```sh
pytest --cov-branch --cov-report term-missing --cov mypackage tests  # requires pytest-cov
coveralls  # requires coveralls and pyyaml installed
```

[Build readthedocs](https://blog.explodinglabs.com/trigger-rtd-build) if
there's been changes.  

Update related blog posts.  
