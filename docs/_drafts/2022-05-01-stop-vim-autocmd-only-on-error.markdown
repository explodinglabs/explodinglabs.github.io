---
layout: post
title: Only show Vim autocmd output on error
permalink: /only-show-vim-autocmd-output-on-error
---
Here we execute `elm make`, but it could be any command that exits with a
non-zero status on error.

```sh
autocmd BufWritePost *.elm silent execute '!elm make '.shellescape('%').' --output docs/elm.js >/dev/null || read -s -k "?Press any key to continue."'
```

## Notes

- `silent` tells Vim not to wait for user input after executing.
- The key part is `|| read`. Note in some shells you can simply use `pause`
  instead of `read -s -k "?Press any key to continue.`. I use zsh which doesn't
  support `read`.
- The `>/dev/null` simply stops outputting stdout output, because we don't care
  about that. We only want to see the errors.
