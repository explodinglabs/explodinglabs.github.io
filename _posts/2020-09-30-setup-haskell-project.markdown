---
layout: post
title: "Setup a Haskell project"
permalink: /haskell/setup
---
This is how I start a new Haskell project.

Initialize stack (creates a new directory, use `--bare` to use current directory).
```sh
stack new myapp
```

Add dependencies to `package.yaml` and then
```sh
stack install
```

Place source files in `app` directory and then
```sh
stack build --file-watch
```

Execute the binary with
```sh
$(stack path --local-install-root)/bin/filename-exe
```
