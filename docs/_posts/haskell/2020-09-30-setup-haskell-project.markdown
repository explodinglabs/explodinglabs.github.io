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

Place source files in `app` directory and then
```sh
stack build
```

Use `stack build --file-watch` to rebuild as your code changes.

Execute the binary with
```sh
stack run myapp
```
