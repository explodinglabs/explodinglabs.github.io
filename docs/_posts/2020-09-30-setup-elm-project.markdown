---
layout: post
title: Setup an Elm project
permalink: /elm/setup
---
<div id="intro" markdown="1">
This is how I setup a new Elm project for development.
</div>

For a Github Pages app, go to Settings > Pages, change Source to Branch: `main`
and directory to `/docs`.

Clone the repository:
```sh
git clone ssh://git@github.com/explodinglabs/myapp
cd myapp
```

Replace "myapp" with the name of your app, in the `README.md`.
Commit and push that change.

Update global npm:
```sh
npm update -g npm
```

Install dev packages:
```sh
npm install --save-dev elm-format elm-review sass
```

```sh
elm-review --template jfmengels/elm-review-unused/example
```

```sh
elm init
```

Create a src/Main.elm.

```sh
elm make src/Main.elm --optimize --output static/elm.js
```

```sh
./node_modules/.bin/uglifyjs static/elm.js --compress 'pure_funcs=[F2,F3,F4,F5,F6,F7,F8,F9,A2,A3,A4,A5,A6,A7,A8,A9],pure_getters,keep_fargs=false,unsafe_comps,unsafe' | ./node_modules/.bin/uglifyjs --mangle --output static/elm.js
```

Add to package.json:
```sh
{
  ...
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "**/*.elm": [
      "elm-format --validate",
      "elm-review"
    ]
  }
}
```

Copy index.html from another project into static/.
Bring up the development container.
Visit http://localhost:80.



To hot-reload, put this in the static/index.html
```html
<script type="text/javascript" src="https://livejs.com/live.js"></script>
```


# Old instructions
[Create a new Github
repository](https://github.com/organizations/explodinglabs/repositories/new),
using the template:

```
explodinglabs/elm-template
```

```sh
npm install --save-dev husky lint-staged elm-format elm-review elm-test sass
npx husky init
npx husky add .husky/pre-commit "npx elm-review"
npx husky install .husky/pre-commit
```

Set the title in `docs/index.html`.
Create a favicon.
Create an opengraph image.

Add the new files to the repository, commit and push.

Follow the instructions in the README to bring up the container.
