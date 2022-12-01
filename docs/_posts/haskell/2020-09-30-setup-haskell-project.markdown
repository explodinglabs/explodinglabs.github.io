---
layout: post
category: haskell
title: Setup a new Haskell project
permalink: /haskell/setup
---
For simple programs with no dependencies, simply create a `.hs` file and
compile it with ghc:

```sh
ghc main.hs && ./main
```

For bigger programs I use Stack.

Initialize Stack (this creates a new directory; use `--bare` to use the current
directory).
```sh
stack new myapp
```

Add any dependencies to `package.yaml` under the "dependencies" section.

Place source files in `app` directory and then:
```sh
stack build
```

To rebuild as code changes:
```sh
stack build --file-watch
```

To rebuild and execute on changes (doesn't work for things that run forever, e.g. servers):
```sh
stack build --file-watch --exec $(stack path --local-install-root)/bin/myapp-exe
```

Execute the binary with
```sh
stack run myapp
```
