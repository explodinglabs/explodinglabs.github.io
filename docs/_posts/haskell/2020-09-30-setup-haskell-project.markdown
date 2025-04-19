---
layout: post
category: haskell
title: How to setup a new Haskell project?
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

To rebuild and execute on changes (doesn't work for things that run forever):
```sh
stack build --file-watch --exec $(stack path --local-install-root)/bin/myapp-exe
```

Execute the binary with
```sh
stack run
```

To find the binary, it's in the "bin" directory here:
```
stack path --local-install-root
```

To install a local module, add it to `stack.yaml` under `packages`:
```
packages:
- .
- ./haskell-mpv
```
And don't forget to add it to package.yaml as a dependency as well. Then build.
