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

For more complete programs I use Stack.

Initialize Stack (creates a new directory, use `--bare` to use the current
directory).
```sh
stack new myapp
```

Add any dependencies to `package.yaml` under the "dependencies" section.

Place source files in `app` directory and then
```sh
stack build --file-watch
```

Execute the binary with
```sh
$(stack path --local-install-root)/bin/filename-exe
```
