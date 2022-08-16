---
layout: post
category: python
title: How to release a new Python package version to PyPI?
permalink: /python/release-to-pypi
---
<div class="wide-logos" markdown="1">
![python](/assets/python.png)
</div>

<div id="intro" markdown="1">
These are the steps I take when releasing a version of my Python package to
PyPI.
</div>

First run your checks/cleaning. I have a post about this
[here](/python/checks). If any fail, start again.

Run tests.
```sh
pytest
rm -r .tox; tox  # Continue below while this is running
```

In a new branch:
- Update version in `setup.py`.
- Update `CHANGELOG.md` (stable releases only).
- Update `README.md`, if any.
- Update documentation.

<div class="warning" markdown="1">
Once the release is uploaded, there's no way to change the `README.md` on PyPI,
or the documentation on Readthedocs, without releasing another version. So take
care with these in stable releases.
</div>

Commit, push and merge into main.
```sh
git commit -a
git push origin head
```

Pull main, tag the commit and push the tag.
```sh
git checkout main
git pull
git tag x.x.x
git push --tags
```

Create the sdist and upload it.
```sh
pip install --upgrade pip setuptools twine
python setup.py sdist
twine check dist/mypackage-x.x.x.tar.gz
twine upload dist/mypackage-x.x.x.tar.gz
```

Update coverage badge.
```sh
pip install --upgrade pytest-cov coveralls pyyaml
pytest --cov-branch --cov-report term-missing --cov mypackage tests
coveralls
```

[Build readthedocs](https://composed.blog/trigger-rtd-build) if there were any
documentation changes.

Update related blog posts/Stack Overflow posts.
