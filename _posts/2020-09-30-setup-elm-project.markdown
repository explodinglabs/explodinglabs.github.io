---
layout: post
title: Setup an Elm project
permalink: /elm/setup
---
This is how I setup a new elm project for development.

In a fresh directory:
```sh
elm init
```

Install elm-live and start server.
```sh
npm init
npm install --save-dev elm-live
node_modules/.bin/elm-live src/Main.elm
```

Install elm-test.
```sh
npm install --save-dev elm-test
elm-test init
```

Install pre-commit hooks.
```sh
npm install --save-dev husky lint-staged
```

Then add to elm.json.
```json
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
  },
```

Elm-review & elm-review-unused.
```sh
npm install --save-dev elm-review
npx elm-review init
cd review
elm install jfmengels/elm-review-unused
```

Then add to `review/src/ReviewConfig.elm`:
```elm
module ReviewConfig exposing (config)

-- import NoUnused.Dependencies
-- import NoUnused.CustomTypeConstructorArgs

import NoUnused.CustomTypeConstructors
import NoUnused.Exports
import NoUnused.Modules
import NoUnused.Parameters
import NoUnused.Patterns
import NoUnused.Variables
import Review.Rule exposing (Rule)


config : List Rule
config =
    [ NoUnused.CustomTypeConstructors.rule []

    -- , NoUnused.CustomTypeConstructorArgs.rule
    -- , NoUnused.Dependencies.rule
    , NoUnused.Exports.rule
    , NoUnused.Modules.rule
    , NoUnused.Parameters.rule
    , NoUnused.Patterns.rule
    , NoUnused.Variables.rule
    ]
```


To build the production `elm.js` file:
```sh
elm make src/Main.elm --optimize --output docs/elm.js
```
