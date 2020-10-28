# Development

Create an elm.json, package.json and tests directory.
```sh
elm init
npm init
```

Install elm-live and start server.
```sh
npm install elm-live
node_modules/.bin/elm-live src/Main.elm
```

Pre-commit.
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

Elm-test
```sh
npm install -g elm-test  # Install elm-test globally first
elm-test init
```

Elm-review & elm-review-unused.
```sh
npm install elm-review
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
