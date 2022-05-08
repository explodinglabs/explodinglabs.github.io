---
layout: post
title: How to install Ormolu in Vim 8 and format when saving?
permalink: /ormolu-vim
---
Install Ormolu:
```sh
stack install ormolu --resolver=lts-15.10
```
Ensure the created binary is in your `$PATH`.

Install Vim plugin:
```sh
git -C ~/.vim/pack/plugins/start clone https://github.com/sdiehl/vim-ormolu
```

Add autocmd to `~/.vimrc`:
```vim
autocmd BufWritePre *.hs :call RunOrmolu()
```
