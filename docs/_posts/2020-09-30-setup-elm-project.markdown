---
layout: post
title: Setup an Elm project
permalink: /elm/setup
---
<div id="intro" markdown="1">
This is how I setup a new Elm project for development.
</div>

[Create a new Github
repository](https://github.com/organizations/explodinglabs/repositories/new),
using the template:
```
explodinglabs/elm-template
```

For a Github Pages app, go to Settings > Pages, change Source to Branch: `main`
and directory to `/docs`.

Clone the repository:
```sh
git clone ssh://git@github.com/explodinglabs/myapp
cd myapp
```

Replace "myapp" with the name of your app, in the `README.md`.
Commit and push that change.

Install npm packages.
```sh
npm init
npm install --save-dev husky lint-staged elm-format elm-review elm-test sass
npx husky add .husky/pre-commit "npx elm-review"
npx husky install .husky/pre-commit
```

Set the title in `docs/index.html`.
Create a favicon.
Create an opengraph image.

Add the new files to the repository, commit and push.

Follow the instructions in the README to bring up the container.
